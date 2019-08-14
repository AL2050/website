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

## The Interface between the Analogue and Digital worlds
We have analogue devices and then we have digital devices. An analogue system transmits continuous information, and in the case of an electronic system, a continuous signal. Digital systems, on the other hand, are configured to transmit and recieve signals that have a discrete number of states.

This is typically achieve through an electronic device known as an Analogue-to-Digital Converter (ADC), which defines a set of discrete states. The analogue waves passing through an ADC is rounded either up or down depending on its value at a specific point.

{:refdef: style="text-align: center;"}
![continuous](https://al2050.github.io/personal-website/assets/cont.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure 1: *You can imagine a continuous signal as being perfectly smooth. There are no steps or jumps throughout its transmission.* 
{:refdef}

{:refdef: style="text-align: center;"}
![discrete](https://al2050.github.io/personal-website/assets/discr.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure 2: *The <span style="color:red">**red line**</span> represents the discrete signal that would be produced, by discretising this signal, in this instance. As you can see, this discrete signal consists of discrete steps. The <span style="color:red">**red line**</span> is the ideal scenario, where the time to transition between states is zero. In reality, a discretised signal would have ramps at the rising and falling edges between discrete states, since it takes a small amount of time to transition from one state to another. The conversion of the **black** signal into the <span style="color:red">**red**</span> signal is achieved through the use of a device called an [Analog-to-Digital Converter][ADC]{:target="_blank"}, to quantise the wave at specific step values*
{:refdef}


It is important to note that naturally, all signals are truly analogue. So, why do we design systems to take these analogue signals and make them digital? Well, by designing circuitry to control signals in a discrete manner enables a higher level of control, efficiency, reliability and precision when computing and storing information.

Digital electronic systems can process and store information much more readily, which is very useful in today's modern digital computers. Also, compared with analogue systems, digital electronics systems are more immune to external noise interference during transmission, that might be experienced, for example, over a communications channel.

The following types of physical devices are in fact possible.

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

## The Idea and Motivation 
The significance of digital circuitry motivated me to design and build an analogue circuit that is the equivalent of a digital NAND-Gate; a component designed to implement what is called [Boolean Logic][boolean]{:target="_blank"}.

{:refdef: style="text-align: center;"}
![blackBox](https://al2050.github.io/personal-website/assets/blackBox.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure 3: *Imagine we have a black box, containing the necessary circuitry to represent a logic gate that obeys Boolean AND logic. There are two or more inputs and a single output. For the output to trigger HIGH/ON, all inputs must also be HIGH/ON. If any input is LOW/OFF, the output will also be LOW/OFF. The inverse conditions are true for a [NAND][nand]{:target="_blank"} gate, a short-hand for NOT-AND gate, where [NOT][not]{:target="_blank"} outputs the inverse of the corresponding input.*
{:refdef}

{:refdef: style="text-align: center;"}
![blackBox-truthTable](https://al2050.github.io/personal-website/assets/blackBoxTruthTable.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure 4: *A table such as this one is called a [truth table][truthTable]{:target="_blank"}. A mathematical logic table relating the inputs to a system with the output.*
{:refdef}

The physical NAND-Gate designed in this project, is a Resistor-Transistor logic (RTL) configuration, using transistors as switches and resistors to regulate voltage and current levels at point in the circuit to agree with the requirements of the two transistors - our inputs - and Light-Emitting Diode (LED) - our output.


#### A brief note on AC-driven electronic systems
Since we are working with a purely DC voltage source, the complexity of the physical system is greatly reduced. We need not worry about parasitic capacitances, transconductance or similar. Also, we are using the transistors as switches, therefore we are not necessarily concerned about performance, as we would if we were designing a voltage amplifier, where precision is essential, or working with high-speed compute, where rapid transistor switching is required.

When dealing with AC electricity, we would refer to the resistance in terms of what is called impedence. Impedence is the effective resistance resulting in an AC-driven environment. 
 
Impedence is mathematically represented as a vector, containing magnitude, which is the resistance caused by the DC offset in the electronic system, and a phase, known as the reactance. 
 
Reactance can be thought of as an opposition to a change in current or voltage, which occurs when an AC signal is transmitted through an electronic system.
 
In this design, these extra details are removed through the use of a DC voltage supply.
 
The benefit of using AC electricity is that an AC voltage can be much more efficiently amplified compared with a DC voltage source. However, we are working with a small electronic system over a very small distance range, and therefore do not require an AC supply.

Before we delve into the specifics of the design, let's first delve into the transistor's internal to gain a deeper understanding into how it is able to behave as a switch, to enable use to create a system that operates under Boolean logic.

## Transistor Internals 101 - <sup><sub><sup><sub><sup><sub>Small</sub></sup></sub></sup></sub></sup> but **MIGHTY**!
{:refdef: style="text-align: center;"}
![smallButMighty](https://al2050.github.io/personal-website/assets/smallButMighty.jpg)
{:refdef}

{:refdef: style="text-align: center;"}
Figure 5: *[Source](https://www.teepublic.com/t-shirt/1774269-superman-letter-t){:target="_blank"}*
{:refdef}


The transistor is well known for being the catalyst of the [Information Age][Information-Age]{:target="_blank"}. It's most common use is as an electronic switch in today's computers, a small but mighty switch that can toggle at exceptionally high rates, while being manufactured at a size, on the low-end of the nano-scale.

There are two sole applications for the transistor.

| Function | Application |
| ---- | ---- |
| As a switch | Automated switching, at high toggle rates, makes this very useful in, for example, the control of a DC motor, [high-power conversion efficiency][highPower]{:target="_blank"} and high switch speeds in low-power components, such as logic gates, which we are looking at in this article. [Here is an interesting discussion on what affects the switching rates of transistors][switchingSpeed]{:target="_blank"}. |
| ---- | ---- |
| As voltage amplifier | Very useful in communications for amplifying signals for transmission (think of the [transceiver][Transceiver]{:target="_blank"}, and in today's communications, [optoelectrical systems][optoElectrical]{:target="_blank"}). |

### Types of Transistor
Several transistor designs have emerged since its physical invention in 1947. [Here is a useful link on the different types of transistor][transistorTypes]{:target="_blank"}.  [MOSFET][mosfet]{:target="_blank"} transistors are currently the most widely used, and are the most commonly used type in microprocessors to date.

The NAND-gate circuit built in this article uses the [BC548 Bipolar-Junction Transistor][BC548-Datasheet]{:target="_blank"}.


### The material that makes the transistor a possibility in this Universe
A semiconductor is a material whose chemical composition is such that it has an [electrical conductivity][conductivity] that is between the range of an insulator such as hard rubber (10^-14 S/m), and a conductor such as copper (~5.96x10^7 S/m).

So how do metals and semiconductors differ structurally on a molecular scale? First, you can visualise a metal as a lattice of bonded metallic cations (positively charged ions), surrounded by a sea of electrons. A semiconductor can also be visualised as a lattice of atoms, but this time with bound electrons and a proportion of these atoms either hold one less or one more electron in their atomic structure, leaving a gap in their regular arrangement. These gaps are known as holes, and are regarded as having a positive electric charge, opposite to that of the electron.

With a sufficient potential difference across a semiconductor, electrons will jump between atoms by occupying these holes, enabling a flow of current through the material and exhibiting conductive properties. There is a threshold voltage that must be met to provide the electrons with enough impetus to enable to jumps between these holes, leading to a flow of current.

[Boron-doped]: http://iamtechnical.com/silicon-lattice-doping-silicon-boron-phosporous
[metallic-structure]: https://www.slideshare.net/ulcerd/chemical-structure-chemical-bonding-ionic-metallic-coordinate-bonds

### The **NP** junction
An N-type semiconductor material has a dominance of electrons in its structure, while a P-type material has a dominance of holes in its structure.

Imagine a segment of N-Type and a segment of P-Type seamlessly connected like so:

{:refdef: style="text-align: center;"}
![NP-Junction](https://al2050.github.io/personal-website/assets/NP_junction.jpg)
{:refdef}

Opposite charges attract and like charges repel. Therefore, if we place a voltage source across the NP-junction like so:

{:refdef: style="text-align: center;"}
![NP-ForwardBias](https://al2050.github.io/personal-website/assets/NP_forwardBias.jpg)
{:refdef}

Then provided we have a sufficient voltage across our NP-junction, a current will flow. This circuit is the equivalent of a diode in the forward bias configuration. The threshold voltage for a diode is typically in the region of [0.6, 0.7] V

{:refdef: style="text-align: center;"}
![NP-ReverseBias](https://al2050.github.io/personal-website/assets/NP_reverseBias.jpg)
{:refdef}

With the diode in reverse bias, something interesting happens. Observing the arragement below, electrons will be flowing in the clockwise direction. Therefore, electrons will be driven towards the N-Type material, while holes while flow towards the P-Type material.

At the interface between the two semiconductor regions, a cloud of holes and electrons forms, as electrons from the left side are forced into the P-Type holes, and holes from the right side are forced to form in the N-Type material. This cloud of holes and electrons shaded in the diagram, is known as the depletion region, and is the breakdown of both semiconductor devices.

When this breakdown takes place, the diode will heat up. Depending on the voltage applied across the diode in reverse bias, the diode may explode due to the rate of depletion, resulting in rapid heating and expansion.

{:refdef: style="text-align: center;"}
![NP-Deplete](https://al2050.github.io/personal-website/assets/NP_deplete.jpg)
{:refdef}

<!--
[How-a-Semiconductor-works-BenEater]: https://www.youtube.com/watch?v=33vbFFFn04k
[How-a-Transistor-works-BenEater]: https://www.youtube.com/watch?v=DXvAlwMAxiA
[hyperPhysics]: http://hyperphysics.phy-astr.gsu.edu/hbase/Solids/dope.html

[semi-conductor_MOS]: https://physics.info/semiconductors/

[pn-junction]: https://en.wikipedia.org/wiki/P%E2%80%93n_junction
-->

<!--
{:refdef: style="text-align: center;"}
![NPN-Explained](https://al2050.github.io/personal-website/assets/NPN.jpg)
{:refdef}
-->


### The NPN sandwich - Back-To-Back diodes
This brings us onto the internals of the transistor.

Take our NP junction from the last section, and now sandwich the P-Type region with a second N-Type segment. This is the equivalent of two back-to-back diodes. Each segment of the NPN sandwich are controlled by a terminal like so:

{:refdef: style="text-align: center;"}
![NPN-BJT](https://al2050.github.io/personal-website/assets/npnbjt.jpg)
{:refdef}


### How does the transistor act like a switch, and why is it useful?
[switch](https://www.quora.com/Why-do-we-use-transistor-as-a-switch){:target="_blank"}
[switch2]: https://www.electronics-tutorials.ws/transistor/tran_4.html

The *bipolar* term in BJT means that there are two polarised regions in the transistor. The BJT is equivalent to two diodes, that are in series in either a back-to-back or a face-to-face arrangement. [Here is a comprehensive article covering the theory behind the diode][diodeTheory].

The BC548 transistor is an NPN transistor. What this means is that 



The name transistor is a portmanteau of the words *transfer* and *resistor*, so transistor etymologically means *transfer resistor*. Resistance isn't physically transferred by a transistor, but, due to the transistor's physical properties, there is a relative difference between the input resistance and the output resistance.

Everything that a transistor can do - namely voltage amplification and switching - is entirely possible to achieve with other components. The transistor has the advantage of being able to do the same things quicker, while being smaller in size, enabling more computation, with lower power - like we see in today's computers - and this can all be achieved at a much higher precision than if we did the same task mechanically.

The transistor we use in this design is the [BC548 transistor][fairchild], manufactured by Fairchild Semiconductor International.

It is an NPN transistor, and is made from semiconductor material.



## Modeling the NAND-Gate circuit

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

[nand]: https://en.wikipedia.org/wiki/NAND_gate

[not]: https://en.wikipedia.org/wiki/Inverter_(logic_gate)

[truthTable]: https://medium.com/i-math/intro-to-truth-tables-boolean-algebra-73b331dd9b94

[highPower]: https://en.wikipedia.org/wiki/Switched-mode_power_supply

[switchingSpeed]: https://www.quora.com/Which-factor-affect-switching-speed-of-transistor

[Transceiver]: https://en.wikipedia.org/wiki/Transceiver

[optoElectrical]: https://en.wikipedia.org/wiki/Heterojunction_bipolar_transistor#Limits

[Potentiometer]: https://www.quora.com/What-is-transferring-resistance-in-reference-to-a-transistor


[Information-Age]: https://en.wikipedia.org/wiki/Information_Age#Innovations

[transistorTypes]: https://www.elprocus.com/different-types-of-transistor-and-their-functions/

[mosfet]: https://www.elprocus.com/mosfet-as-a-switch-circuit-diagram-free-circuits/



[BC548-Datasheet]: https://al2050.github.io/personal-website/assets/BC548.pdf


[diodeTheory]: https://www.allaboutcircuits.com/textbook/semiconductors/chpt-3/introduction-to-diodes-and-rectifiers/


[fairchild]: https://www.onsemi.com/products/discretes-drivers/general-purpose-and-low-vcesat-transistors/bc548


[ADC]: https://en.wikipedia.org/wiki/Analog-to-digital_converter#Resolution

[conductivity]: https://www.thoughtco.com/table-of-electrical-resistivity-conductivity-608499


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