---
layout: default
title: SystemVerilog on macOS
permalink: /notes/comp_arch/iverilog_dep
lastmod: 2026-02-13
---
[← ../Computer_Architecture](../comp_arch)

## SystemVerilog on macOS & Makefile
_Last modified: {{ page.lastmod | date: "%b %d, %Y" }}_

### Icarus Verilog (iverilog):
This is your compiler for system verilog. You can [homebrew](https://formulae.brew.sh/formula/icarus-verilog) this. \
** make sure you have vvp

### GTKwave:  
if you already tried installing through brew...

```
brew uninstall gtkwave
brew untap randomplum/gtkwave
brew install --HEAD randomplum/gtkwave/gtkwave
```

### Running the files:

First you need to compile the file
```
iverilog -g2012 -o simulation.vvp tb_example.sv example.sv
```
* -g2012 for systemVerilog 2012 features
* -o to specify output file

Then execute the file with
```
vvp simulation.vvp
```

to view the waves
```
gtkwave simulation.vcd
```

note that to view the wave, you need to add dumpfiles and dumpvars in your testbench file. \
Also, as you might have noticed this is not fun. So let's use makefile.

### Makefile:
first, create a file that is called `Makefile`. \
I recommend using [this](https://github.com/robmarano/verilog_project_template/tree/main).
few things that needed to be changed:

```
simulate: $(COMPONENT).vvp 
@echo "Simulating component: $(COMPONENT)"
	$(SIMULATOR) $(SFLAGS) $(COMPONENT).vvp #$(SOUTPUT) 
```

comment out the $(SOUTPUT) part \
Also I added `*.vvp` on my clean

### Example:
![example_usage.png](./assets/comp_arch_makefile.png)

→ to compile \
`make COMPONENT=tb_example_module.sv compile` 

→ to run \
`make COMPONENT=tb_example_module.sv simulate` 

→ to display (GTKwave) \
`make COMPONENT=example_module display` 

→ to clean \
`make COMPONENT=example_module clean` 

** Notice how it is still not that great of a makefile. But I don't know Makefile well enough yet.

