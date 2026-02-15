---
layout: default
title: SystemVerilog on macOS
permalink: /notes/comp_arch/sverilog01
lastmod: 2026-02-14
---
[← ../Computer_Architecture](../comp_arch)

# Learning SystemVerilog 01
_Last modified: {{ page.lastmod | date: "%b %d, %Y" }}_

## Example
Well... I had to learn SystemVerilog. And this is something that I made while trying to learn it. \
The original code was from Prof. Marano's [website](https://robmarano.github.io/courses/ece251/2026/weeks/week_04/notes_week_04.html) \
I just spammed some comments, but I thought some might find it helpful.

```c
module my_module (
    input logic         clk,     // single bit signal
    input logic         rst,
    input logic [3:0]   data_in, // 4 bit signal MSB:3 , LSB: 0 
    output logic [3:0]  data_out 
);

    // here we define internal signals, parameters and types before using them
    logic [3:0] internal_signal;
    localparam WIDTH = 4;
    // this just decalres local varisable called WIDTH and making it 4. 
    // though it is not used in here anyways.

    // Dataflow: continuous assignment
    assign internal_signal = ~data_in;  // ~ is bitwise not

    // this is making sequential logic here
    always_ff @(posedge clk) begin
        if (rst) 
            data_out <= 4'b0; // alway_ff you use <= but alwasy_comb you use =
        else
            data_out <= internal_signal;
    end

endmodule

// to test this logic, we need testbench.
// --> let's go to tb_my_module.sv
```
Think this code as your "device." To test your device, you need some other stuff to test it out, and we call thie test bench. 
The following is an example test bench for the code that was presented above. 

```c
`timescale 1ns/1ps // this defines time unit / precision
                   // time unit defines what #1 means, in this case 1ns
                   // time precision is the smalleset unit that simulator can
                   // represent

module tb_my_module; // components that you want to test should be declared here

    // DUT signals, *dut meaning design under test (DUT: Device Undet Test)
    // here you are declaring variables to connect to DUT.
    // don't do input logic clk or output logic ... because that is not the module
    logic clk;
    logic rst;
    logic [3:0] data_in;
    logic [3:0] data_out;

    // Instantiate DUT
    // This is like wiring things together
    my_module dut(
        .clk(clk), // testbench clk --> DUT clk, * inside_the_module(testbench_variable)
        .rst(rst),
        .data_in(data_in),
        .data_out(data_out)     
    );

    initial clk = 0;        // initialize clk to be 0
    always #5 clk = ~clk;    // you made a clock nice 

    // dump waves (for GTKwave)
    initial begin
        $dumpfile("wave.vcd");
        $dumpvars(0, tb_my_module);
    end

    // ------------------------------------
    // Nice job, now you have initilized your testbench
    // ------------------------------------

    initial begin
        $display("time | rst | clk | data_in | data_out |");
        $monitor("t=%0t| rst=%b | clk=%b | data_in=%h | data_out=%h", $time, clk, rst, data_in, data_out);
        // think display and monitor as a printf of c.
        // display only prints out the test, and monitor is how you print variables with printf.

        // t for time
        // b for bindary
        // h for hex


        rst = 1;
        data_in = 4'h0; //4 bits, hexadecimal base, A is the number

        repeat (2) @(posedge clk);
        rst = 0;
        // it holds rst = 0 for 2 pos edge clock

        // let's test some values
        data_in = 4'hA; @(posedge clk);
        data_in = 4'h0; @(posedge clk);
        data_in = 4'hB; @(posedge clk);
        
        $finish; //you need this to finish it
    end

endmodule 
```

Another useful thing that I wanted to mention is that when you have several input variables, you can make something that is really similar to the truth table:

```c
initial a = 0;
always #5 a = ~a;

initial b = 0;
always #10 b = ~b;

initial c = 0;
always #20 c = ~b;
//and so on...
```