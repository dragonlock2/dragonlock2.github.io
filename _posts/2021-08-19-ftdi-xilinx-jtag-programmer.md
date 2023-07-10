---
title: FTDI Xilinx JTAG Programmer
date: 2021-08-19
categories: projects
excerpt: Thanks to some netizens dumping FTDI EEPROMs, I was able to hack together my own Xilinx programming cables.
header:
  teaser: /assets/img/2021/ft232h_real.jpg
---

Literally the day before starting my summer internship, I decided to teach myself how to use Altium Designer. I decided to try something relatively simple and use up the FT232H chips that I bought almost a year ago. The FT232H, FT2232H, and FT4232H make up an interesting family of chips that appears to have a partial monopoly in the FPGA dev board world due to their MPSSE which can emulate a variety of interfaces. For my first board designed with a mouse in the past 3 years, the board came out pretty good.

## Schematic

The schematic is pretty simple, with the FT232H not requiring too many external components and the datasheet even providing example circuits. As is the theme with most of the boards I design at home, I ignored standard things like ferrite beads, TVS, and fuses due to board size and not having parts. In addition to standard decoupling, the FT232H needs a “precision” 12K resistor (I just put a 10K and 1Ks in series), a 12MHz crystal, and EEPROM.

{% include figure image_path="/assets/img/2021/ft232h_schematic.png" %}

## Layout

Altium’s layout software is pretty awesome. I really like the quick switching between 3D views which makes it really easy to find and correct things like silkscreen overlap. The live DRC pointing out part collisions is also nice. It can be a bit annoying to set up design rules and having to press two keys for everything instead of one for KiCad but overall, I like it. It didn’t take long before I had a completed layout.

{% include figure image_path="/assets/img/2021/ft232h_layout.png" %}

## Flashing EEPROMs

The secret sauce that turns an FTDI chip into a Xilinx programmer is just special values stored in its EEPROM which alerts Xilinx/Digilent drivers to configure it as such. While I would certainly recommend against recreating my project in a commercial capacity without legal agreements with Xilinx or Digilent, for the struggling college student or someone who opposes the partial monopoly on a moral basis, it just might be worth it.

I have to give credit to this [gist](https://gist.github.com/rikka0w0/24b58b54473227502fa0334bbe75c3c1) which was the only reason this project was possible (especially since I didn’t own any official programmers myself). I’ve compiled all of the EEPROM dumps along with some of my own in a central repo just in case the original gist disappears.

<https://github.com/dragonlock2/ftdi_dumps>

{% include figure image_path="/assets/img/2021/ft232h_real.jpg" %}
