---
layout: post
title:  "From Natural Sciences to User Interface - Part 1"
<!--date:   2019-08-09 12:00:00 +0100-->
categories: Analogue-Electronics
tags: [hardware, electronics-projects, logic-gates]
---

The objective of this series is to provide a holistic insight into the operations of a general-purpose computer from the physical principles governing the semi-conductor technologies that form the DNA of each and every transistor, all the way up to the User-Interface, the final output that is represented on a screen such as the one you are reading this article on right now! So let's get cracking!

First, here is an itinerary of the topics we will be covering in this article series.

# Part 1 of 5
1. The physical principles governing transistors and how they are manufactured.

2. The fundamental digital electronic components and their properties that make them useful, as well as the advantages and disadvantages between them (Voltage regions, material characteristics, operations / functions)

3. Digital Logic - from Analogue to Digital circuitry (AND, OR, NOT...; circuit design, circuit theory...)

---

# Part 2 of 5
1. Digital memory - from combinational to sequential digital circuitry - the essence of enabling compute.

2. Binary logic systems (How they works, and how it is all possible)

---

# Part 3 of 5
* Computer Architecture (CPU, IO, Peripherals)

---

# Part 4 of 5
* Operating Systems (How they communicate with the hardware?, What makes software possible?; WinAPI, Boot Loaders..., Paging)

---

# Part 5 of 5
1. OSI model (Hardware layer to the Application layer)

2. Extending beyond the end-user - Networking and Communication Technologies (their protocols, architecture(routers, DNS,...))

---

(Could also talk about the evolution of code from low-level to high level somewhere in this series. (Bootstraping, UNIX, C, Assembly (Architecture specific)))

(Could also do a video YouTube demonstration of NAND gate circuit design - link to a seperate article outlining the design process undertook and the result for the NAND gate - this article will be linked where we talk about the NAND gate.)

---
# Part 1
Have you ever wondered what is inside a logic gate? In digital electronics, a logical NAND gate, for example, is represented diagrammatically in the following manner:

{:refdef: style="text-align: center;"}
![NAND-gate-symbol](https://al2050.github.io/personal-website/assets/nandGate.png)
{: refdef}

But, what lies under the hood of this mysterious symbol? In this article, we are going to explore the NAND gate, how it works and why it is configured the way it is. We are looking at the NAND gate because, in electronics, this gate is known as a universal gate, ['meaning that any other gate can be represented as a combination of NAND gates'.][nandLogic-wiki]{:target="_blank"} This is also known as [functional completeness][functional-completeness]{:target="_blank"}.



In today's computers, the typical circuitry used to represent a logic gate involves the use of what are called, Metal Oxide Semiconductor Field-Effect Transistor, or MOSFET for short.



[nandLogic-wiki]: https://en.wikipedia.org/wiki/NAND_logic#Making_other_gates_by_using_NAND_gates

[functional-completeness]: https://en.wikipedia.org/wiki/Functional_completeness

