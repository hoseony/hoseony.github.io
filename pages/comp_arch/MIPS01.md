---
layout: default
title: SystemVerilog on macOS
permalink: /notes/comp_arch/MIPS01
lastmod: 2026-02-15
---
[← ../Computer_Architecture](../comp_arch)

# MIPS 01 [WIP]
_Last modified: {{ page.lastmod | date: "%b %d, %Y" }}_

I think I will be talking about some random MIPS stuff.

## Basic Formatitng 
```s
.data
    example_variable: .word 0

.text
.globl main

main:
    #end program
    li $v0, 10
    syscall 
```


## Testing / Compiling
[JsSpim](https://shawnzhong.github.io/JsSpim/)
This is very good online MIPS emulator. I found this more useful and user friendly than homebrew spim that I was originally using. 


## Syscall
While I was working on the homework, I found this website: [syscall reference](https://hwlabnitc.github.io/MIPS/mips_syscalls&tutorial). It is very well documented.

## Stack Pointer
These two videos gave me enough explanation. 
* [SP1](https://youtu.be/yvGIYG6zYQA?si=8V4cCK3Iw_ZLxAjz)
* [SP2](https://youtu.be/ewpo1NERc3o?si=R9fB534AdwfxuEkH)