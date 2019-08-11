---
layout: post
title:  "Using the Transistor as a Voltage Amplifier"
<!--date:   2019-08-09 12:00:00 +0100-->
categories: Digital-Electronics
tags: [hardware, electronics-projects, logic-gates]
---

# How does the transistor act like a switch, and why is it useful?
[switch][https://www.quora.com/Why-do-we-use-transistor-as-a-switch]




Everything that a transistor can do is entirely possible to achieve with other components. The transistor has the advantage of being able to do the same things quicker, while being smaller in size, enabling more computation, with lower power, like we see today in computers, and this can all be achieved at a much higher precision than if your did so mechanically.

For example, we could set up a potentiometer with one end tied to a collector voltage, **Vcc**, and the wiper of the potentiometer connected to ground. If we then move the wiper from one end to the other, we change the input impedence


{:refdef: style="text-align: center;"}
![pot1](https://al2050.github.io/personal-website/assets/pot.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure #: Picture a potentiometer from a birds-eye view. The wiper of the potentiometer is represented by the <span style="color:red">**red arrow**</span>. The wiper controls the resistance level, by acting like a variable potential divider circuit.
{: refdef}

{:refdef: style="text-align: center;"}
![pot2](https://al2050.github.io/personal-website/assets/pot2.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure #: As the arrow moves clockwise, the resistance will increase, and therefore, the output voltage will also increase for the same current passing through the potentiometer.
{: refdef}

{:refdef: style="text-align: center;"}
![potChange1](https://al2050.github.io/personal-website/assets/potChange1.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure #: We can represent this change in resistance mathematically like so.
{: refdef}

{:refdef: style="text-align: center;"}
![potChange2](https://al2050.github.io/personal-website/assets/potChange2.png)
{:refdef}

{:refdef: style="text-align: center;"}
Figure 6: This change in resistance will result in a change in voltage, proprotional to the change in the resistance, by Ohm's Law.
{: refdef}

