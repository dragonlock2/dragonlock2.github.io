---
title: Spartan 7 Breakout
date: 2021-08-19
categories: projects
excerpt: During the great chip shortage of 2021, I decided it was about time I designed something with an FPGA on it.
header:
  teaser: /assets/img/2021/spartan7_3.jpg

gallery:
  - image_path: /assets/img/2021/spartan7_1.jpg
  - image_path: /assets/img/2021/spartan7_2.jpg
  - image_path: /assets/img/2021/spartan7_4.jpg
---

After seeing so many SpaceX designs with Xilinx parts and taking EE151, I decided to try my hand at building a breakout for one myself. I also wanted to play around with LVDS which most dev boards don’t break out. At the end of they day, the process felt very similar to what I usually do with microcontrollers except having to go through a bunch more documentation.

## Schematic

Given the whole chip shortage, the hardest part of this project was just finding parts that were in stock and were cheap enough that I could absorb development costs. I wanted to use a Spartan 7 which hits that balance of price and performance and bought an XC7S15-1CSGA225I. This is the first time I’ve purchased parts before even starting the schematic because my other choices went out of stock. For the programmer, the FT2232H everyone uses is out of stock so I used an FT4232H which strangely has a lot of stock. I guess companies tend not to need the 4 MPSSEs the FT4232H offers. I know I didn’t. Anyway, here’s the schematic PDF.

[Spartan7_Breakout.pdf](/assets/pdf/Spartan7_Breakout.pdf)

{% include figure image_path="/assets/img/2021/spartan7_top.png" %}

Much like the [K66F Breakout](https://matthewtran.dev/2021/08/k66f-breakout/), I tried to keep sheets organized for design reuse. For the connectors, I used 22 pin FFC for LVDS so I can use cables from Amazon and a JTAG header in case I want to experiment with programming Lattice chips. This is also the first time I’ve intentionally added TVS to a design.

7-series chips need power sequencing and after spending an hour looking for the smallest and cheapest solution, I settled on just sequencing the cheapest buck regulator on Digikey with power goods and enables. The datasheet for the regulator calculated the wrong recommended resistor values so this is the first time I’ve directly disobeyed a datasheet. Technically I didn’t obey the power off sequence requirements due to size but it hasn’t caused me issues yet. If I were doing this properly I’d probably invest time into learning how to use PMICs or trying out a power sequencer chip with a system monitor to kill things quickly on sudden power disconnect. For a future design I guess.

Hooking up the FPGA was relatively straightforward it was really just loads of documentation. Just like microcontrollers, you just need to hook up power, clocks, config pins (and flash in this case), JTAG, and any peripherals you want. I really like Xilinx’s pinout files since I can basically copy paste them into Altium to make a symbol. I didn’t follow decoupling suggestions to the letter due to size (100uF caps are huge) but it worked out. Sadly, the FT4232H doesn’t offer a clock output like the FT2232H does so this is the first time I added a MEMS oscillator to a design.

## Layout

I can safely say that layout was quite difficult. Due to size, I moved to 0402 and 0201 parts for everything. While I hate soldering QFPs, I have to say being able to route things underneath it makes life a lot easier. Getting the 0.8mm BGA part routed was a bit hard because I obeyed OSH Park’s 5mil trace/space rule which prevented routing traces between vias. For my next design I’ll definitely move to 4mil or 4.5mil traces which according to other peoples’ experiences is reliable. Overall, I’m pretty happy with how the layout turned out and how I fit it on a 4 layer board while maintaining size.

{% include figure image_path="/assets/img/2021/spartan7_layout.jpg" %}

## Assembly

Stencils really are quite awesome. This is the first time I’ve soldered a QFP chip without any pins bridging. I did have a bunch of tombstoning on one of the boards but a little bit of hot air got that fixed. My first board initially didn’t work and man was I stressed until I realized the decoupling cap on the input power didn’t reflow properly. Considering there were other decoupling caps nearby, I’m surprised by how much it mattered.

{% include gallery %}

Everything ended up working! Well I haven’t tested the LVDS nor the non-UART FTDI pins yet but I’ll get there when I do something with it. For the 5th board I’ve designed in the past 3 years with a mouse, I have to say I’m pretty proud of it.

{% include figure image_path="/assets/img/2021/spartan7_overall.jpg" %}
