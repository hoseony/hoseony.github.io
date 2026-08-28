---
layout: default
title: Projects
permalink: /projects/
---

<section class="projects-list-page">
  <h1>Projects</h1>

  <div class="projects-showcase-grid">
    <article class="project-showcase">
      <div class="project-showcase-heading">
        <h2>cfish</h2>
        <a href="https://github.com/hoseony/cfish">GitHub</a>
      </div>
      <p>A chess engine written in C with a GUI built using raylib. Built with Thomas George.</p>
      <div class="project-showcase-image project-showcase-photo">
        <img src="/assets/projects/cfish-example.png" alt="cfish chess GUI screenshot">
      </div>
    </article>

    <article class="project-showcase">
      <div class="project-showcase-heading">
        <h2>Pico RP2350 UART Driver</h2>
        <a href="https://github.com/hoseony/pico-rp2350-UART-driver">GitHub</a>
      </div>
      <p>A polling-based UART (Universal Asynchronous Receiver-Transmitter) driver for the RP2350 microcontroller, implemented using minimal Pico SDK abstractions. UART relies on an agreed baud rate rather than a shared clock line and uses independent transmit (TX) and receive (RX) data paths.</p>
      <ul class="project-showcase-details">
        <li>Implemented UART initialization, baud-rate configuration, and RX/TX control.</li>
      </ul>
      <div class="project-showcase-image project-showcase-diagram">
        <img src="/assets/projects/rp2040uart.png" alt="UART transmit and receive waveform">
      </div>
    </article>

    <article class="project-showcase">
      <div class="project-showcase-heading">
        <h2>16-bit Pipelined CPU</h2>
        <a href="https://github.com/hoseony/ECE251-Final-Project">GitHub</a>
      </div>
      <p>A custom-ISA pipelined CPU inspired by MIPS and the Intel 8080, written in SystemVerilog. Built with Evan Dong.</p>
      <div class="project-showcase-image project-showcase-diagram">
        <img src="/assets/projects/cpu-diagram.png" alt="16-bit pipelined CPU diagram">
      </div>
    </article>

    <article class="project-showcase">
      <div class="project-showcase-heading">
        <h2>Digital Etch-A-Sketch</h2>
        <a href="/assets/projects/etch-a-sketch.pdf">PDF</a>
      </div>
      <p>An Etch-A-Sketch built with digital logic and simulated in Logisim Evolution. Built with Evan Dong.</p>
      <div class="project-showcase-image project-showcase-photo">
        <img src="/assets/projects/etch-a-sketch-web.jpg" alt="Digital Etch-A-Sketch breadboard circuit">
      </div>
    </article>
  </div>
</section>
