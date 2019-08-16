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
We have analogue systems and then we have digital systems. An analogue system transmits continuous information, and in the case of an electronic system, a continuous signal. Digital systems, on the other hand, are configured to transmit and receive signals that have a discrete number of states.

The conversion of a continuous signal to a digital signal is typically achieved through an electronic device known as an Analogue-to-Digital Converter (ADC), which defines a set of discrete states that are allowed to exist. The analogue waves passing through an ADC is rounded either up or down depending on its value at a specific point.

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
Figure 2: *The <span style="color:red">**red line**</span> represents the discrete signal that would be produced, by discretising this signal, in this instance. As you can see, this discrete signal consists of discrete steps. The <span style="color:red">**red line**</span> is the ideal scenario, where the time to transition between states is zero. In reality, a discretised signal would have ramps at the rising and falling edges between discrete states, since it takes a small amount of time to transition from one state to another. The conversion of the **black** signal into the <span style="color:red">**red**</span> signal is achieved through the use of a device called an [Analog-to-Digital Converter][ADC]{:target="_blank"}, to quantise the wave at specific step values*.
{:refdef}


It is important to note that naturally, all signals are innately analogue. So, why do we design systems to take these analogue signals and make them digital? Well, by designing circuitry to control signals in a discrete manner enables a higher level of control, efficiency, reliability and precision when computing and storing information.

Digital electronic systems can process and store information much more readily, which is very useful in today's modern digital computers. Also, compared with analogue systems, digital electronics systems are more immune to external noise interference during transmission, that might be experienced, for example, over a communications channel.

A notable downside to digital systems is a higher power consumption.

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
Figure 3: *Imagine we have a black box, containing the necessary circuitry to represent a logic gate that obeys Boolean AND logic. There are two or more inputs and a single output. For the output to trigger HIGH/ON, all inputs must also be HIGH/ON. If any input is LOW/OFF, the output will also be LOW/OFF. The inverse conditions are true for a [NAND][nand]{:target="_blank"} gate, or a NOT-AND gate, where [NOT][not]{:target="_blank"} outputs the inverse of the corresponding input.*
{:refdef}

{:refdef: style="text-align: center;"}
![blackBox-truthTable](https://al2050.github.io/personal-website/assets/blackBoxTruthTable.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure 4: *A table such as this one is called a [truth table][truthTable]{:target="_blank"}. A mathematical logic table relating the inputs to a logical system with the output. This is the truth table for a general NAND gate.*
{:refdef}

The physical NAND-Gate designed in this project, is a Resistor-Transistor logic (RTL) configuration, using transistors as switches and resistors to regulate voltage and current levels at points in the circuit, to agree with the electronic requirements of the two transistors - our inputs - and Light-Emitting Diode (LED) - our output.


#### A brief note on AC-driven electronic systems
Since we are working with a purely DC voltage source, the complexity of the physical system is greatly reduced. We need not worry about parasitic capacitances, transconductance or similar. Also, we are using the transistors as asynchronous switches, therefore we are not necessarily concerned about performance, as we would if we were designing a voltage amplifier, where precision is essential, or working with high-speed compute, where rapid transistor switching and optimal timing is required.

When dealing with AC electricity, we would refer to the resistance in terms of what is called impedence. Impedence is the effective resistance resulting in an AC-driven environment. 
 
Impedence is mathematically represented as a vector, containing magnitude, which is the resistance caused by the DC offset in the electronic system, and a phase, known as the reactance. Reactance can be thought of as an opposition to a change in current or voltage, which occurs when an AC signal is transmitted through an electronic system.
 
In this design, these extra details are removed through the use of a DC voltage supply.
 
The benefit of using AC electricity is that an AC voltage can be much more efficiently amplified compared with a DC voltage source. However, we are working with a small electronic system over a very small distance range, and therefore do not require an AC supply.

In fact, the power supply unit in your PC converts the AC mains electricity from your mains supply to DC power supply, used to power your PC.

Before we delve into the specifics of the NAND-gate design, let's first explore the internals of one type of transistor to gain a deeper understanding into how it is able to behave as a switch, which will provide us with a foundation for creating an Analogue system that operates under Boolean logic.

## Transistor Internals 101 - <sup><sub><sup><sub><sup><sub>Small</sub></sup></sub></sup></sub></sup> but **MIGHTY**!
{:refdef: style="text-align: center;"}
![smallButMighty](https://al2050.github.io/personal-website/assets/smallButMighty.jpg)
{:refdef}

{:refdef: style="text-align: center;"}
Figure 5: *[Source](https://www.teepublic.com/t-shirt/1774269-superman-letter-t){:target="_blank"}*
{:refdef}

The name transistor is a portmanteau of the words *transfer* and *resistor*, so transistor etymologically means *transfer resistor*. Resistance isn't physically transferred by a transistor, but, due to the transistor's physical properties, there is a relative difference between the input resistance and the output resistance. The is due to the physical make-up of a transistor, and is what enables the transistor to amplify voltages. We will explore this make-up shortly.

The transistor is well known for being the catalyst of the [Information Age][Information-Age]{:target="_blank"}. It's most common use is as an electronic switch in today's computers, a small but mighty switch that can toggle at exceptionally high rates, while being manufactured at a size, on the low-end of the nano-scale.

There are two sole applications for the transistor.

| Function | Application |
| ---- | ---- |
| As a switch | Automated switching, at high toggle rates, makes this very useful in, for example, the control of a DC motor, [high-power conversion efficiency][highPower]{:target="_blank"} and high switch speeds in lower-power components, such as logic gates, which we are looking at in this article. [Here is an interesting discussion on what affects the switching rates of transistors][switchingSpeed]{:target="_blank"}. |
| ---- | ---- |
| As voltage amplifier | Very useful in communications for amplifying signals for transmission (think of the [transceiver][Transceiver]{:target="_blank"}, and in today's communications, [optoelectrical systems][optoElectrical]{:target="_blank"}). |

### Types of Transistor
Several transistor designs have emerged since its physical invention in 1947. [Here is a useful link on the different types of transistor][transistorTypes]{:target="_blank"}.  [MOSFET][mosfet]{:target="_blank"} transistors are currently the most widely used, and are the most commonly used type in microprocessors to date.

The NAND-gate circuit built in this article uses the [BC548 Bipolar-Junction Transistor][BC548-Datasheet]{:target="_blank"}. [Click here to read more about the uses and benefits of implement Bipolar-Junction Transistors.][BJT-applications]


### The material that makes the transistor a possibility in this Universe
A semiconductor is a material whose chemical composition is such that it has an [electrical conductivity][conductivity] that is between the range of an insulator such as hard rubber (10^-14 S/m), and a conductor such as copper (~5.96x10^7 S/m).

So how do metals and semiconductors differ structurally on a molecular scale? First, you can visualise a metal as a lattice of bonded metallic cations (positively charged ions), surrounded by a sea of negatively charged electrons. A semiconductor can also be visualised as a lattice of atoms, but this time with bound electrons and a proportion of these atoms either hold one less or one more electron in their atomic structure, leaving a gap in their regular arrangement. These gaps are known as holes, and are regarded as having a positive relative electric charge, opposite to that of the electron.

With a sufficient potential difference across a semiconductor, electrons will jump between atoms by occupying these holes, enabling a flow of current through the material and exhibiting conductive properties. There is a threshold voltage that must be met to provide the electrons with enough impetus to enable to jumps between these holes, leading to a flow of current.

[Boron-doped]: http://iamtechnical.com/silicon-lattice-doping-silicon-boron-phosporous
[metallic-structure]: https://www.slideshare.net/ulcerd/chemical-structure-chemical-bonding-ionic-metallic-coordinate-bonds

### The **NP**  Junction Semiconductor
An N-type semiconductor material has a dominance of electrons in its structure, while a P-type material has a dominance of holes in its structure.

Imagine a segment of N-Type and a segment of P-Type seamlessly connected like so:

{:refdef: style="text-align: center;"}
![NP-Junction](https://al2050.github.io/personal-website/assets/NP_junction.jpg)
{:refdef}

Opposite charges attract and like charges repel. Therefore, if we place a voltage source across the NP-junction like so:

{:refdef: style="text-align: center;"}
![NP-ForwardBias](https://al2050.github.io/personal-website/assets/NP_forwardBias.jpg)
{:refdef}

Then provided we have a sufficient voltage across our NP-junction, a conventional current will flow in the clockwise direction. Conventional current is a standard that refers to current as flowing from positive to negative. This is the opposite the the flow of electrons which is from negative to positive. In the proceeding sections we will be refering to conventional current.

|Type|Direction|
|----|----|
|Conventional current|**+** to **-**|
|----|----|
|Flow of electrons|**-** to **+**|

This circuit is the equivalent of a diode in the forward bias configuration. The threshold voltage for a diode is typically in the region of [0.6, 0.7] V.

Observing the above NP semiconductor arrangement, the polarity of the NP material provides a polarity in net charge and so a current will successfully flow through the material, with a sufficient potential difference across it. Hence the semi-conductor will begin to conduct.

{:refdef: style="text-align: center;"}
![NP-ReverseBias](https://al2050.github.io/personal-website/assets/NP_reverseBias.jpg)
{:refdef}

With the diode in reverse bias, something interesting happens. Observing the arragement above, electrons will be flowing in the clockwise direction. Therefore, electrons will be driven towards the N-Type material, while holes while flow towards the P-Type material.

At the interface between the two semiconductor regions - known as the NP-Junction - a cloud of holes and electrons forms, as electrons from the left side are forced into the P-Type holes, and holes from the right side are forced to form in the N-Type material. 

Heat is produced, and breakdown of the material takes place, as shown in the depiction below. This cloud of holes and electrons shaded in the diagram, is known as the depletion region, and is the breakdown of both semiconductor devices.

When this breakdown takes place, the diode will heat up, and depending on the voltage applied across the diode in reverse bias, the diode may explode due to the rate of depletion, resulting in rapid heating and expansion.

{:refdef: style="text-align: center;"}
![NP-Deplete](https://al2050.github.io/personal-website/assets/NP_deplete.jpg)
{:refdef}


### The NPN sandwich - Back-To-Back diodes
This brings us onto the internals of the Bipolar-Junction-Transistor.

Take our NP segment from the last section, and now sandwich the P-Type segment with a second N-Type segment. This is the equivalent of two back-to-back diodes. 

{:refdef: style="text-align: center;"}
![NPN-BJT](https://al2050.github.io/personal-website/assets/b2b_diodes.jpg)
{:refdef}

Each segment of the NPN sandwich is controlled by a terminal like so:

{:refdef: style="text-align: center;"}
![NPN-BJT](https://al2050.github.io/personal-website/assets/npnbjt.jpg)
{:refdef}

The *Bipolar* term in BJT means that there are two polarised regions in the transistor. The BJT is equivalent to two diodes, that are in series in either a back-to-back or a face-to-face arrangement. [Here is a comprehensive article covering the theory behind the diode][diodeTheory].

#### Why make the sandwich?
Let's apply a voltage across our NPN sandwich like we did with the NP-segment above.

{:refdef: style="text-align: center;"}
![1-BJT](https://al2050.github.io/personal-website/assets/1bjt.jpg)
{:refdef}

The resistor, R<sub>c</sub>, is our controller for the flow of conventional current that will be driven downwards, into the upper N-Type segment of our NPN sandwich. Different BJT components have different allowed current ranges that they can safely operate with. To determine these ranges, engineers refer to [datasheets][BC548-Datasheet]{:target="_blank"}.

Applying a supply voltage to the upper N-Type segment, we will find that minimal, if any, conventional current flows downwards due to there being an insufficient amount of holes occupying the lower N-Type segment. 

In order for the conventional current to flow from the V<sub>cc</sub> supply and through the NPN transistor to ground, we must apply a sufficient conventional current to the B line, known as the Base of the transistor. This increases the number of holes in the P-Type segment, promoting holes in the lower N-type segment, further polarising the NPN transistor, where it becomes more negative in the top N-Type segment.

When this happens, holes can more readily enter the upper N-Type segment from the V<sub>cc</sub> supply, and since there will be an abundance of holes now in the lower N-Type segment, the result is an amplified net current flowing from V<sub>cc</sub> to ground.

This is kind of like building up electrical momentum in the downwards direction, and is equivalent to closing a manual electrical switch.

Characteristically, only a small conventional current at the base is required to achieve a significantly larger conventional current through the NPN transistor. 

<!--
Generally, the P-Type region is small than either of the N-Type regions, but large enough to enable sub-atomic particles to gain enough momentum to pass through the NPN composite.
-->

The transistor we use in this design is the [BC548 transistor][fairchild], manufactured by Fairchild Semiconductor International.

### Why not just use a switch? Why do we need a transistor?
Everything that a transistor can do - namely voltage amplification and switching - is entirely possible to achieve with other components. The transistor has the advantage of being able to do the same things quicker, while being smaller in size, enabling more computation, with lower power comsumption per component - like we see in today's computers - and this can all be achieved at a much higher precision than if we did the same task mechanically.


## Modeling the NAND-Gate circuit
So now that we understand how a BJT can behave like an electronic switch, let's now devise a model for our logical NAND-gate circuit.

Below are a set of visual depictions to describe the logical function of the transistor arrangement proposed.

{:refdef: style="text-align: center;"}
![2-switches](https://al2050.github.io/personal-website/assets/twoSwitches.jpg)
{:refdef}

{:refdef: style="text-align: center;"}
Figure #: The <span style="color:red">**red circles**</span> represent holes, while the <span style="color:green">**green dashes**</span> represent electrons. Two BJTs are connected in series, with collector... upper... lower... ground...
{:refdef}

The design in this article is for a 2-input 1-output NAND-gate. Therefore, we require two switches for the inputs to represent the HIGH/ON and LOW/OFF states. In order to control our transistor switches, we must supply their Base terminals with a current source. The way we do this here is by connecting the Base terminals to their own resistors of which are connected to the supply voltage.

{:refdef: style="text-align: center;"}
![NAND Gate Circuit Model in Multisim](https://al2050.github.io/personal-website/assets/NAND-Gate-Circuit-Model.JPG)
{:refdef}

{:refdef: style="text-align: center;"}
Figure #: 
{: refdef}




{:refdef: style="text-align: center;"}
![zerozero](https://al2050.github.io/personal-website/assets/zerozero.jpg)
{:refdef}

{:refdef: style="text-align: center;"}
Figure #: 
{: refdef}

{:refdef: style="text-align: center;"}
![zeroone](https://al2050.github.io/personal-website/assets/zeroone.jpg)
{:refdef}

{:refdef: style="text-align: center;"}
Figure #: 
{: refdef}

{:refdef: style="text-align: center;"}
![onezero](https://al2050.github.io/personal-website/assets/onezero.jpg)
{:refdef}

{:refdef: style="text-align: center;"}
Figure #: 
{: refdef}

{:refdef: style="text-align: center;"}
![oneone](https://al2050.github.io/personal-website/assets/oneone.jpg)
{:refdef}

{:refdef: style="text-align: center;"}
Figure #: 
{: refdef}



## Building the NAND-Gate circuit on a Bread-Board
{:refdef: style="text-align: center;"}
![Physical-NAND-Gate-Circuit](https://al2050.github.io/personal-website/assets/NAND_Gate_Circuit.jpg)
{:refdef}


{:refdef: style="text-align: center;"}
![Demonstration-Video](https://www.youtube.com/channel/UCHi9Cyd8CSJhyiRbS8FKXAg/videos?view_as=subscriber)
{:refdef}

{:refdef: style="text-align: center;"}
Figure #: Video here
{: refdef}


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

[BJT-applications]: https://en.wikipedia.org/wiki/Bipolar_junction_transistor#Applications


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