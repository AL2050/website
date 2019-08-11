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
Figure #: You can imagine a continuous signal as being perfectly smooth. There are no steps or jumps throughout its transmission. 
{:refdef}

{:refdef: style="text-align: center;"}
![discrete](https://al2050.github.io/personal-website/assets/discr.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure #: The <span style="color:red">**red line**</span> represents the discrete signal that would be produced, by discretising this signal, in this instance. As you can see, this discrete signal consists of discrete steps. The <span style="color:red">**red line**</span> is the ideal scenario. In reality, a discretised signal would have ramps at the rising and falling edges between discrete states.
{:refdef}


It is important to note that naturally, all signals are truly analogue. So, why do we design systems to take these analogue signal and make them digital? Well, by designing circuitry to control signals in a discrete manner enables a higher level of control, efficiency, reliability and precision when computing and storing information.

Digital electronic systems can process and store information much more readily, which is very useful in today's modern digital computers. To add to that, compared with analogue systems, digital electronics systems are more immune to signal noise, that might be experienced, for example, over a communications channel.

The following types of system are in fact possible.

|Type|Example|
|-----|
|Analogue Non-Electronic Devices|Pendulum Clocks, Speedometers|
|-----|
|Digital Non-Electronic Devices|[The Lehmer Sieve][Lehmer]{:target="_blank"}|
|-----|
|Analogue Electronic Devices|[Crystal Radio Receivers][Crystal]{:target="_blank"}|
|-----|
|Digital Electronic Devices|[Modern Computers][Modern-Computers]{:target="_blank"} (PC's, Mobile Phones)|
|-----|

The significance of digital circuitry motivated me to design and build a circuit that is the equivalent of a NAND-Gate; a logic gate, which is a component designed to implement what is called [Boolean Logic][boolean]{:target="_blank"}.

{:refdef: style="text-align: center;"}
![blackBox](https://al2050.github.io/personal-website/assets/blackBox.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure #: The logical operator AND, for example, means that if we have a black box, with two or more inputs and one output, then for the output to trigger HIGH, all inputs must also be HIGH. If any one of those inputs is LOW, then the output will be LOW. The inverse is true for NAND (NOT-AND).
{:refdef}

{:refdef: style="text-align: center;"}
![blackBox-truthTable](https://al2050.github.io/personal-website/assets/blackBoxTruthTable.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure #: A table such as this one is called a *truth table*. A mathematical logic table relating the inputs to a system with the output.
{:refdef}

The physical NAND-Gate has been designed in it's simplest form as a Resistor-Transistor logic configuration, using transistors as switches and resistors to control voltage and current levels.

Since we are working with a purely DC voltage source, the complexity of the physical system is greatly reduced. We need not worry about parasitic capacitances, transconductance or similar. Also, we are using the transistors as switches, therefore we are not necessarily concerned about performance, as we would if we were designing a voltage amplifier, where precision is essential.

Before we delve into the specifics of the design, let's see how the transistor makes digitisation of analogue signals readily achievable.

## The Theory of the Transistor - Small but Mighty
The transistor is well known for being the catalyst of the [Information Age][Information-Age]{:target="_blank"}. It's most common use is as an electronic switch in today's computers, a small but mighty switch that can toggle at exceptionally high rates, while being manufactured at a size, on the low-end of the nano-scale.

The two applications for the transistor.

| Function | Application |
| ---- | ---- |
| As a switch | Automated switching, at high toggle rates, makes this very useful in, for example, the control of a DC motor, [high-power conversion efficiency](https://en.wikipedia.org/wiki/Switched-mode_power_supply){:target="_blank"} and high switch speeds in low-power components, such as logic gates, which we are looking at in this article. |
| ---- | ---- |
| As voltage amplifier | Very useful in communications (think of the [transceiver][Transceiver]{:target="_blank"}). |


### What's inside a transistor?
The name transistor is a portmanteau of the words *transfer* and *resistor*, so transistor etymologically means *transfer resistor*. Resistance isn't physically transferred by a transistor, but, due to the transistor's physical properties, there is a relative difference between the input resistance and the output resistance.


#### A brief note on AC-driven electronic systems
 
 When dealing with AC electricity, we would refer to the resistance in terms of what is called impedence. Impedence is the effective resistance resulting in an AC-driven environment. 
 
 Impedence is mathematically represented as a vector, containing magnitude, which is the resistance caused by the DC offset in the electronic system, and a phase, known as the reactance. 
 
 Reactance can be thought of as an opposition to a change in current or voltage, which occurs when an AC signal is transmitted through an electronic system.
 
 In this design, these extra details are removed through the use of a DC voltage supply.
 
 The benefit of using AC electricity is that an AC voltage can be much more efficiently amplified compared with a DC voltage source. However, we are working with a small electronic system over a very small distance range, and therefore do not require an AC supply.


### How does the transistor act like a switch, and why is it useful?
[switch](https://www.quora.com/Why-do-we-use-transistor-as-a-switch){:target="_blank"}

Everything that a transistor can do is entirely possible to achieve with other components. The transistor has the advantage of being able to do the same things quicker, while being smaller in size, enabling more computation, with lower power - like we see today's in computers - and this can all be achieved at a much higher precision than if we did than mechanically.

#### So, how can we use a transistor as a switch?

The transistor we use in this desin is the [BC548 transistor][fairchild], manufactured by Fairchild Semiconductor International.

It is an NPN transistor. 

[How-a-Semiconductor-works-BenEater]: https://www.youtube.com/watch?v=33vbFFFn04k
[How-a-Transistor-works-BenEater]: https://www.youtube.com/watch?v=DXvAlwMAxiA

{:refdef: style="text-align: center;"}
![NPN-Explained](https://al2050.github.io/personal-website/assets/NPN.jpg)
{:refdef}


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


[boolean]: https://www.lotame.com/what-is-boolean-logic/

[Transceiver]: https://en.wikipedia.org/wiki/Transceiver

[Potentiometer]: https://www.quora.com/What-is-transferring-resistance-in-reference-to-a-transistor


[Information-Age]: https://en.wikipedia.org/wiki/Information_Age#Innovations

[fairchild]: https://www.onsemi.com/products/discretes-drivers/general-purpose-and-low-vcesat-transistors/bc548





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