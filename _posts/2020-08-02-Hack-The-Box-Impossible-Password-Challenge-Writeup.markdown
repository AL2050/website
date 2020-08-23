---
layout: post
title: "HITB - Impossible Password Writeup"
categories: Reverse Engineering
---

<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.15.6/styles/default.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.15.6/highlight.min.js"></script>
<script>hljs.initHighlightingOnLoad();</script>

# Tools used to solve this challenge

|---|---|
|Technology|Description|
|---|---|
|<a href="https://www.virtualbox.org/" target="_blank">VirtualBox</a> (Ubuntu 19.10 (Eoan Ermine) Virtual Machine)|Virtualisation to provide a sufficiently secure environment for HITB Reverse Engineering challenges|
|---|---|
|*<a href="https://github.com/tmux/tmux/wiki" target="_blank">tmux</a>*|For partitioning terminal windows|
|*<a href="https://ghidra-sre.org/" target="_blank">Ghidra</a>*|Disassembler|
|---|---|
|<a href="https://man7.org/linux/man-pages/man1/strings.1.html" target="_blank">*strings* command</a>|Data gathering from binary file's mapped to memory|
|---|---|
|<a href="https://man7.org/linux/man-pages/man1/file.1.html" target="_blank">*file* command</a>|Provides us with potentially useful information about the type of binary file.|
|---|---|

# Challenge Message

*Are you able to cheat me and get the flag?*

---

# Walk-Through

The first thing to do is download the zip archive for this challenge and <a href="https://en.wikipedia.org/wiki/File_verification" target="_blank">verify the authenticity</a> of the downloaded file by its SHA256 checksum.

The extracted file is a binary file. My first move is to run the binary file against the file command, to determine the kind of binary file we are dealing with. The binary file is an <a href="https://upload.wikimedia.org/wikipedia/commons/e/e4/ELF_Executable_and_Linkable_Format_diagram_by_Ange_Albertini.png" target="_blank">executable ELF file</a>

{:refdef style="text-align: center;"}
![file-command]({{ site.url }}/personal-website/assets/HITB-writeups/Impossible-Password/HITB-password-file.png){:height="100%" width="100%"}
{:refdef}

Notice that the file has been stripped. This is most likely to make debugging it the binary more of a challenge.

{:refdef style="text-align: center;"}
![strings-command]({{ site.url }}/personal-website/assets/HITB-writeups/Impossible-Password/HITB-password-strings.png){:height="75%" width="75%"}
{:refdef}

*strings* shows us the standard header information and strings stored in the binary executable file. A few strings
stand out here.

- **<span style="color:red">SuperSeKretKey</span>:** This hints at a key that might be used when the program is run.
- **<span style="color:green">%20s</span>:** This looks like some formatting based upon the <span style="color:green">%</span> symbol and the same with <span style="color:green">[%s]</span>.
- **<a href="https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux" target="_blank">Red Hat</a> with <span style="color:blue">GCC</span>:** an executable compiled from C code. Also the presence of <a href="https://refspecs.linuxbase.org/LSB_3.1.0/LSB-generic/LSB-generic/baselib---libc-start-main-.html" target="_blank">__libc_start_main</a> in the strings output indicates that a main() function is present in this C program.

There is also malloc for memory allocation and strcmp to compare strings which could be used for password verification, if for example
this executable recieves user input.

## Static Analysis

Now, we have some tangible information about the type of binary file we are working with and some useful strings that we can use a signposts, we can now dig deeper into the behaviour of our binary. For this, I will use Ghidra.

{:refdef style="text-align: center;"}
![Ghidra]({{ site.url }}/personal-website/assets/HITB-writeups/Impossible-Password/Ghidra.png){:height="40%" width="40%"}
{:refdef}

Since the binary file has been stripped, the main function was not interpreted directly by Ghidra, so working through the disassembly I deduced which function was *main()*. I then read through the disassembly for each function called in *main()* and renamed them based upon what I think they are doing and converted the local variables to characters for ease of readability. This is the result.

<pre>
<code class="c">
void main(void) {
       int iVar1;
       char *stage2_str;
       byte local_48;
       undefined local_47;
       undefined local_46;
       undefined local_45;
       undefined local_44;
       undefined local_43;
       undefined local_42;
       undefined local_41;
       undefined local_40;
       undefined local_3f;
       undefined local_3e;
       undefined local_3d;
       undefined local_3c;
       undefined local_3b;
       undefined local_3a;
       undefined local_39;
       undefined local_38;
       undefined local_37;
       undefined local_36;
       undefined local_35;
       char user_input [20];
       int local_14;
       char *stage1_str;

       stage1_str = "SuperSeKretKey";
       local_48 = 'A';
       local_47 = ']';
       local_46 = 'K';
       local_45 = 'r';
       local_44 = '=';
       local_43 = '9';
       local_42 = 'k';
       local_41 = '0';
       local_40 = '=';
       local_3f = '0';
       local_3e = 'o';
       local_3d = '0';
       local_3c = ';';
       local_3b = 'k';
       local_3a = '1';
       local_39 = '?';
       local_38 = 'k';
       local_37 = '8';
       local_36 = '1';
       local_35 = 't';

       printf("* ");

       __isoc99_scanf(&format,user_input);

       printf("[%s]\n",user_input);

       local_14 = strcmp(user_input,stage1_str);
       if (local_14 != 0) {
       	  	  exit(1);
       }
       printf("** ");

       __isoc99_scanf(&format,user_input);
       stage2_str = (char *)generate_second_key(0x14);
       iVar1 = strcmp(user_input,stage2_str);

	if (iVar1 == 0) {
	   	print_decrypted_flag(&local_48);
	}
	return;
}
</code>
</pre>

*printf()*, *scanf()* and *strcmp()* were all determined by Ghidra. ```generate_second_key()``` and ```print_decrypted_flag```
were renamed manually based upon what I thought these function are doing. ```generate_second_key()``` is interesting. It uses
C's rand() in-built function and conducts some kind of re-ordering or data. However, as you will see in the Dynamic Analysis
below, I bypassed this function to retrieve the HITB flag.

## Dynamic Analysis

Above, we discovered that the binary file has been <a href="https://medium.com/@tr0id/working-with-stripped-binaries-in-gdb-cacacd7d5a33" target="_blank">stripped</a>. This means a flag was set during compilation that directs the compiler to discard
debugging symbols. Therefore, we are required to manually determine the entrypoint to the program.

For Dynamic Analysis, I am using <a href="https://www.gnu.org/software/gdb/" target="_blank">GDB</a>.

We can do this with either the ```info file``` or the ```info target``` command.

{:refdef style="text-align: center;"}
![info-file]({{ site.url }}/personal-website/assets/HITB-writeups/Impossible-Password/HITB-password-gdb-info-file.png){:height="75%" width="75%"}
{:refdef}

So our entrypoint to the program is at the address ```0x4006a0``` in hex. In other words, the program data starts at this
location in memory. Our objective is to arrive at the main() function, which we need to find.

{:refdef style="text-align: center;"}
![break-at-entrypoint]({{ site.url }}/personal-website/assets/HITB-writeups/Impossible-Password/break-at-entrypoint.png){:height="30%" width="30%"}
{:refdef}

Setting a breakpoint at ```0x4006a0``` and typing and returning ```r``` (short for run), the program is run up to this memory location. To display the binary diassembly in GDB for a stripped file, we can run the following command.

{:refdef style="text-align: center;"}
![20instructions]({{ site.url }}/personal-website/assets/HITB-writeups/Impossible-Password/20instructions.png){:height="60%" width="60%"}
{:refdef}

If you are working with a file that is not stripped, you can run ```disas main``` for example where ```disas``` is short for
disassemble.

{:refdef style="text-align: center;"}
![ghidra-entrypoint]({{ site.url }}/personal-website/assets/HITB-writeups/Impossible-Password/ghidra-entrypoint.png){:height="75%" width="75%"}
{:refdef}

In Ghidra, I identified that the main function is not called directly. Instead, ```main()``` is passed into the RDI register
before ```__libc_start_main``` is called. This is probably a form of obfuscation on the ```main()``` function. Cross-referencing
the dis-assembly in Ghidra with GDB, the main function must reside at the location ```0x40085d``` in memory.

{:refdef style="text-align: center;"}
![gdb-to-main]({{ site.url }}/personal-website/assets/HITB-writeups/Impossible-Password/gdb-to-main.png){:height="40%" width="40%"}
{:refdef}

Setting a breakpoint at ```main()``` and continuing there with the command ```c``` (short for continue), and displaying the
disassembly.

{:refdef style="text-align: center;"}
![gdb-main]({{ site.url }}/personal-website/assets/HITB-writeups/Impossible-Password/gdb-main.png){:height="50%" width="50%"}
{:refdef}

At the beginning of ```main()```, twenty characters are mapped contiguously onto the stack. These characters make up an
encrypted form of the HITB flag. ```print_decrypted_flag()``` is responsible for the decryption of this flag, and returns
the key to <a href="https://man7.org/linux/man-pages/man3/stdout.3.html" target="_blank">stdout</a>.

<pre>
<code class="c">
       ...
       printf("* ");

       __isoc99_scanf(&format,user_input);

       printf("[%s]\n",user_input);

       local_14 = strcmp(user_input,stage1_str);
       if (local_14 != 0) {
       	  	  exit(1);
       }
       printf("** ");

       __isoc99_scanf(&format,user_input);
       stage2_str = (char *)generate_second_key(0x14);
       iVar1 = strcmp(user_input,stage2_str);

	if (iVar1 == 0) {
	   	print_decrypted_flag(&local_48);
	}
	return;
}
</code>
</pre>

The Ghidra disassembly above showed us that there are two key stages in the program. If you were to run the program, you 
would be initially presented with an asterix. The program then awaits input from the user. Granted your input matches ```stage1_str```, which turns out to be *SuperSeKretKey*, you succeed to the second stage.

<pre>
<code class="c">
void * generate_second_key(int param_1) {
	int iVar1;
	time_t tVar2;
	void *pvVar3;
	int local_c;
  
	tVar2 = time((time_t *)0x0);
	DAT_00601074 = DAT_00601074 + 1;
	srand(DAT_00601074 + (int)tVar2 * param_1);
	pvVar3 = malloc((long)(param_1 + 1));

  	if (pvVar3 != (void *)0x0) {
    	   	 local_c = 0;
		 while (local_c < param_1) {
		         iVar1 = rand();
			 *(char *)((long)local_c + (long)pvVar3) = (char)(iVar1 % 0x5e) + '!';
			 local_c = local_c + 1;
		}
		*(undefined *)((long)pvVar3 + (long)param_1) = 0;
    		return pvVar3;
  	}
	exit(1);
}
</code>
</pre>

We can set a breakpoint at the instruction where the user's input is tested against the second key generated by 
```generate_second_key()```. This way, the program will run us through the second stage of the program, and the value we
return does not matter as we will see.

At the second stage of the program, the user is presented with two asterix characters in stdout and awaits input from the user
, like in the first stage. This time, however, the key is randomly generated. In order to print the decrypted flag,
```iVar1``` must resolve to zero. ```iVar1``` is the return value from ```strcmp``` which is stored in the ```rax``` register.
 Therefore, we can trick the program into thinking that we provide it with the key that ```generate_second_key()``` has
generated, by setting the ```rax``` to zero before continuing the program.

We can use the ```layout regs``` command to provide us with a view of the values in the processor's general purpose registers.

{:refdef style="text-align: center;"}
![layout-regs]({{ site.url }}/personal-website/assets/HITB-writeups/Impossible-Password/layout-regs.png){:height="75%" width="75%"}
{:refdef}

Let's set the ```rax``` register to zero.

{:refdef style="text-align: center;"}
![set-rax-0]({{ site.url }}/personal-website/assets/HITB-writeups/Impossible-Password/set-rax-0.png){:height="20%" width="20%"}
{:refdef}

{:refdef style="text-align: center;"}
![rax-register]({{ site.url }}/personal-website/assets/HITB-writeups/Impossible-Password/rax-register.png){:height="30%" width="30%"}
{:refdef}

If we now continue the program, we are presented with the decrypted flag.

{:refdef style="text-align: center;"}
![HTB-flag]({{ site.url }}/personal-website/assets/HITB-writeups/Impossible-Password/HTB-flag.png){:height="30%" width="30%"}
{:refdef}
