---
title: "Porting SST on Nucleo F303"
date: 2023-05-29
tags: []
publish: false
---

The Quantum Framework, developed by Miro Samek, is a software framework designed for building event-driven, reactive embedded systems. It provides a structured approach to software development, emphasizing modularity, reusability, and scalability.

At the core of the Quantum Framework is the concept of hierarchical state machines (HSMs), which are used to model the behavior of the system. HSMs allow for the representation of complex system behaviors in a hierarchical and modular manner, making it easier to understand and maintain the software.

# Super Simple Tasker
Instead of moving to this full fledge framework from bare metal programs. Super simple tasker also known as hardware based RTOS.
Using nested vectore controller features to simulate preemptive kernel, also saving overhead of private stack for each task.

# Porting on Nucleo board F303
Example code provided in SST repository [SST](https://github.com/QuantumLeaps/Super-Simple-Tasker) for nucleo l053 controller. Below are steps I followed
for porting blinky example F303.

After creating standard project in STM32CubeIDE using seperate INC/SRC structre.
## Imported kernel files from below folders to respective
INC/SRC folders.
1. sst.c
2. sst_port.c from (ports/arm-cm)
3. sst_port.h from (ports/arm-cm)
4. sst.h
5. dbc_assert.h
6
## Import bsp files
1. bsp_nucleo-l053r8.c
This file uses basic low level drivers. In order to make it HAL compatible and to
map LED 2 on nucleo board made changes to device specific header file and called initialization
from MX library.

## Main.c
Finally copied the main.c from example folder.
