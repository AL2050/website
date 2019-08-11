---
layout: post
title:  "A NAND Gate created using Analogue Circuitry"
<!--date:   2019-08-09 12:00:00 +0100-->
categories: Analogue-Electronics
tags: [hardware, electronics-projects, logic-gates]
---

<!--## Template
* The Idea and Motivation
* The Theory
* Modeling the Circuit
	* White Board Design (screenshots - complement explanations with digital drawings)
	* NI Multisim modeling and simulation (print of circuit and results)
*Physical build of circuit and Test (Testing circuit in stages at each stage of the build process) - what are the sub-systems of the circuit?
-->

<!--Explain what is involved if we used an AC voltage source. Why don't we need it? What do general-purpose computers use? AC?-->

## Idea and motivation
We have analogue devices and then we have digital devices. An analogue system transmits continuous information, and in the case of an electronic system, a continuous signal. Digital systems, on the other hand, are configured to transmit and recieve signals that have a discrete number of states.

{:refdef: style="text-align: center;"}
![continuous](https://al2050.github.io/personal-website/assets/cont.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure 1: You can imagine a continuous signal as being perfectly smooth. There are no steps, or jumps its 
{:refdef}

{:refdef: style="text-align: center;"}
![discrete](https://al2050.github.io/personal-website/assets/discr.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure 2: The <span style="color:red">**red line**</span> represents the discrete signal that would be produced in this instance.
{:refdef}


It is important to note that naturally, all signals are truly analogue. So, why do we design systems to take these analogue signal and make them digital? Well, by designing circuitry to control signals in a discrete manner enables a higher level of control, efficiency, reliability and precision when computing and storing information.

Digital electronics systems can process and store information much more readily, which is very useful in today's modern digital computers. To add to that, digital electronics systems are more immune, than analogue systems, to signal noise that might be experienced over a communications channel, for example.

The following combinations are in fact possible.

|Type|Example|
|-----|
|Analogue Non-Electronic Devices|Pendulum Clocks, Speedometers|
|-----|
|Digital Non-Electronic Devices|[The Lehmer Sieve][Lehmer]{:target="_blank"}|
|-----|
|Analogue Electronic Devices|[Crystal Radio Recievers][Crystal]{:target="_blank"}|
|-----|
|Digital Electronic Devices|[Modern Computers][Modern-Computers]{:target="_blank"} (PC's, Mobile Phones)|
|-----|

The significance of digital circuitry motivated me to design and build a circuit that is the equivalent of a NAND-Gate; a logic gate, which is a component designed to implement what is called Boolean Logic, such as AND, OR, NOT, and so on.

AND, for example, means that if we have a black box, with two or more inputs and one output, then for the output to trigger HIGH, all inputs the the black box must also be HIGH. If any one of those inputs is LOW, then the output will be LOW.


{:refdef: style="text-align: center;"}
![blackBox](https://al2050.github.io/personal-website/assets/blackBox.png)
{:refdef}

{:refdef: style="text-align: center;"}
![blackBox-truthTable](https://al2050.github.io/personal-website/assets/blackBox_truthTable.png)
{:refdef}



This systems has been designed in it's simplest form as a Resistor-Transistor logic configuration, using transistors as switches and resistors to control voltage and current values, to agree with the specifications of the transistors used, which will be explained in the next section.

Since we are working with a purely DC voltage source, the complexity of the physical system is greatly reduced. We need not worry about parasitic capacitances, transconductance or similar. Also, we are using the transistors as switches, therefore we are not necessarily concerned about performance, as we would if we were designing a voltage amplifier, where precision is essential.


## The Theory of the Transistor - Small but Mighty
The transistor is well known as being the catalyst of the [Information Age][Information-Age]{:target="_blank"}. It's most common use is as an electronic switch in today's computers, a small but mighty switch that can toggle at exceptionally high rates, while being manufactured on the low-end of the nano-scale.

The two applications for the transistor.

| Function | Application |
| ---- | ---- |
| As a switch | Automated switching, at high toggle rates, makes this very useful in, for example, the control of a DC motor, [high-power conversion efficiency](https://en.wikipedia.org/wiki/Switched-mode_power_supply){:target="_blank"} and high switch speeds in low-power components, such as logic gates, which we are looking at in this article. |
| ---- | ---- |
| As voltage amplifier | Very useful in communications (think of the [transceiver][Transceiver]{:target="_blank"}). |


### What's inside a transistor?
The name transistor is a portmanteau of the words *transfer* and *resistor*, so transistor etymologically means *transfer resistor*. Resistance isn't physically transferred by a transistor, but, due to the transistor's physical properties, there is a relative difference between the input impedence and the output impedence.

#### How is this possible, and why is it useful?

Everything that a transistor can do is entirely possible to achieve with other components. The transistor has the advantage of being able to do the same things quicker, while being smaller in size, enabling more computation, with lower power, like we see today in computers, with logic gates, and can be aachieved at a much higher precision.

For example, set up a potentiometer with one end tied to a collector voltage, **Vcc**, and the wiper of the potentiometer connected to ground. Now, if we then move the wiper from one end to the other, we change the input impedence


{:refdef: style="text-align: center;"}
![pot1](https://al2050.github.io/personal-website/assets/pot.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure 3: Picture a potentiometer from a birds-eye view. The wiper of the potentiometer is represented by the red arrow. The wiper controls the resistance level, by acting like a variable potential divider circuit. As the red arrow moves clockwise, the resistance will increase, and therefore, the output voltage will also increase for the same current passing through the potentiometer.
{: refdef}

{:refdef: style="text-align: center;"}
![pot2](https://al2050.github.io/personal-website/assets/pot2.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure 4: 
{: refdef}

{:refdef: style="text-align: center;"}
![potChange1](https://al2050.github.io/personal-website/assets/potChange1.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure 5: 
{: refdef}

{:refdef: style="text-align: center;"}
![potChange2](https://al2050.github.io/personal-website/assets/potChange2.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure 6: 
{: refdef}


## Modeling the NAND-Gate circuit

{:refdef: style="text-align: center;"}
[BC548-Datasheet](https://al2050.github.io/personal-website/assets/BC548.pdf){:target="_blank"}
{:refdef}

{:refdef: style="text-align: center;"}
![NAND Gate Circuit Model in Multisim](https://al2050.github.io/personal-website/assets/NAND-Gate-Circuit-Model.JPG)
{:refdef}

{:refdef: style="text-align: center;"}
Figure #: 
{: refdef}

## Building the NAND-Gate circuit on a Bread-Board

{:refdef: style="text-align: center;"}
![Physical-NAND-Gate-Circuit](https://al2050.github.io/personal-website/assets/NAND_Gate_Circuit.jpg)
{:refdef}





[NAND-Gate-Design]: https://www.electronics-tutorials.ws/logic/logic_5.html


[Lehmer]: https://en.wikipedia.org/wiki/Lehmer_sieve
[Crystal]: https://en.wikipedia.org/wiki/Crystal_radio
[Modern-Computers]: https://en.wikipedia.org/wiki/Universal_Turing_machine#Stored-program_computer


[Transceiver]: https://en.wikipedia.org/wiki/Transceiver

[Potentiometer]: https://www.quora.com/What-is-transferring-resistance-in-reference-to-a-transistor


[Information-Age]: https://en.wikipedia.org/wiki/Information_Age







<!--
['The similarity between linear mechanical components, such as springs and dashpots (viscous-fluid dampers), and electrical components, such as capacitors, inductors, and resistors is striking in terms of mathematics. They can be modeled using equations of the same form.'](https://en.wikipedia.org/wiki/Analog_computer#Electronic_analog_computers){:target="_blank"}


['In electronics, a digital-to-analog converter (DAC or D-to-A) is a circuit for converting a digital signal (usually binary) to an analog signal (current, voltage or electric charge). Digital-to-analog converters are interfaces between the digital world and analog world. An analog-to-digital converter (abbreviated ADC, A/D or A to D) is an electronic circuit that converts continuous signals to discrete digital numbers.'](https://en.wikipedia.org/wiki/Analog_device#Interfacing_the_digital_and_analog_worlds){:target="_blank"}
-->


<!--
### ADCs - The interface between the Analogue and the Digital worlds
An Analogue-To-Digital converter essentially takes out the continuity in the analgoue signal. It is removing the unneccesary intermediate voltages between the threshold values between logic '0', 'Undefined' and logic '1'.
-->


<!--Digital devices is founded upon the design of electronic circuitry to operate-->


<!--A computer is essential what? A device that does some kind of calculations in either an Analogue or a digital format.-->