---
layout: default
title: 01 Blinky
permalink: /notes/embedded/blinky01
lastmod: 2026-06-17
---
[← ../Embedded](../embedded)

# 01 Blinky
_Last modified: {{ page.lastmod | date: "%b %d, %Y" }}_

To start off this project, I decided to write a bare-metal blinky program using the built-in LED on the STM32F407 Discovery board. I will use this page to collect notes as I learn more about bare-metal embedded development this summer.

## General Resources
- [STM32World bare-metal development](https://stm32world.com/wiki/STM32_Bare_Metal_Development)
- [Bare-Metal Programming Guide](https://github.com/cpq/bare-metal-programming-guide)

## src/stm32f407.ld
The linker script describes how the final program should be laid out in memory. For bare-metal programming, this matters because there is no operating system loading the program for you.

- [sourceware.org: Linker Script](https://sourceware.org/binutils/docs/ld/Scripts.html)
- [osdev.org: Linker Script](https://wiki.osdev.org/Linker_Scripts)
- [STM32CUBEF4 (github)](https://github.com/PaxInstruments/STM32CubeF4/blob/master/Projects/STM32F4-Discovery/Applications/FatFs/FatFs_USBDisk/SW4STM32/STM32F4-DISCO/STM32F407VGTx_FLASH.ld)

## Bootstrapping
When you start a computer, it has to go through a sequence of stages before it can run a program. You can think of bootstrapping as the work that happens between starting up a computer and running `main`.

### `__attribute__`
`__attribute__` is a GNU C extension that lets you attach extra information to functions, variables, types, or labels. In bare-metal programming, it is useful because you often need to control exactly where something is placed in memory, how it is aligned, or how the compiler generates code.

The attributes I have seen so far:

- `__attribute__((__aligned__(x)))`: aligns a memory address to a multiple of `x`.
- `__attribute__((weak))`: allows the symbol to be overridden by another definition.
- `__attribute__((section("section_name")))`: forces something into a specific section in the object file.

Other attributes that might be useful:
- `naked`: omits the standard function prologue and epilogue sequence when generating assembly.
- `noreturn`: tells the compiler that this function never returns.

## RCC (Reset and Clock Control)
The programmer needs to specify which peripherals they want to use. This is done through RCC, and it also saves power by keeping unused peripherals disabled.

The GPIO peripheral will not respond until its clock is enabled. Even if the GPIO registers are memory-mapped, writing to them will not do anything useful if the peripheral clock is off.

The general flow for using a GPIO port looks like this (for the blinky):

1. Enable the GPIO port clock through `RCC_AHB1ENR`.
2. Configure the pin mode in the GPIO `MODER` register.
3. Write to the output register to turn the LED on or off.

For example, if the LED is on a pin from GPIO port D, then GPIOD's clock needs to be enabled first. After that, the GPIO configuration registers can be used normally.

When something does not seem to be working, checking RCC first might be helpful.