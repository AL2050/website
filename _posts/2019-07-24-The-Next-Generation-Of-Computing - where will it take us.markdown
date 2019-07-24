---
layout: post
title:  "The Next Generation of Computation - where will it take us?"
date:   2019-07-16 18:49:00 +0100
categories: jekyll update
---
Graphcore. A new and novel start-up company, on a mission to develop an entirely new processor, with the goal of accelerating the growth of innovations in the fields of Artificial Intelligence (AI), and much more.

This article is a reiteration of a talk presented by Simon Knowles, the CTO and co-founder of Graphcore, at the RAAIS Conference in London, 2017, of which you can find [here][Graphcore-talk] / [here][RAAIS-talk]

There are two major processing components in a computer that executes all computational processes. The Central Processing Unit, and the Graphics Processing Unit.

While the CPU is designed to execute instructions provided by a computer program, to achieve a certain operation or output, and a GPU is designed to efficiently [WIKI] ‘manipulate and alter memory to accelerate the creation of images’, Graphcore’s Intelligence Processing Unit (IPU) is instead designed, to process what are known as Graphs, which is the primary mode of expression for understanding, implementing and evolving Machine Learning in computational systems.

Simon Knowles describes the IPU as follows, “An IPU-style machine is a pure, distributed, parallel processor.” It is designed so that, “we can build little ones, big ones, and in the future, really, really big ones, and it will still be the same machine.”

Let’s break down what this means.

* First, the IPU is ‘pure’, meaning it is designed purely for Artificial Intelligence applications. The IPU does not deal with any graphics or High-Performance Computing (HPC) applications like GPU’s, and is designed purely for Machine Learning purposes. It is a “Memory-Centric power device”. 

* Second, the IPU is distributed. In other words, the IPU holds thousands of little localised processor and memory modules that all process and exchange information (We will elaborate on this characteristic below.)

* Third, the IPU is parallel, meaning all those little processing units compute parts of the program simultaneously. Once complete, they all exchange messages before repeating the cycle (see Bulk Synchronous Parallel, below.)

* Finally, the IPU’s design characteristics make it readily scalable into very large systems in the near future.

Next, let’s delve deeper into the IPU’s architecture, and discover the motivations behind its design.

Under the hood, the IPU consists entirely of many independent little processors, with their own localised memory, that can send messages to each other through what Simon calls, “a completely stateless, perfect interconnect”. This means that nothing in the IPU is shared, which makes for HUGE parallelism. “There is no shared scheduler, as scheduling is achieved by the compiler” -  as opposed to scheduling directly in the processing unit, which is what occurs in a CPU and GPU - “and there is no shared memory, because this would limit scalability.”

![Figure 1: As you can see, the IPU comprises of two parts. The Random-Access-Memory (RAM), where information is stored and retrieved, and the Floating-Point-Unit (FPU), where arithmetic operations take place on the data. Remember, both memory and processor are distributed (see Figure 2)]({{site.url}}{{site.baseurl}}/assets/IPU.jpg)


[Graphcore-talk]: https://www.youtube.com/watch?v=T8DvHnb3Y9g
[RAAIS-talk]: https://www.youtube.com/watch?v=Gh-Tff7DdzU
