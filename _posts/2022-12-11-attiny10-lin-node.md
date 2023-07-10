---
title: ATtiny10 LIN Node
date: 2022-12-11
categories: projects
excerpt: Since LIN transceivers are glorified level translators and LIN is slow enough to bit-bang, I built a LIN node using an ATtiny10.
header:
  teaser: /assets/img/2022/attiny10_lin.jpg
---

<https://github.com/dragonlock2/kicadboards/tree/main/tests/attiny10_lin>
<https://github.com/dragonlock2/miscboards/tree/main/microchip_studio/attiny10_lin/attiny10_lin>

After building my first [LIN device](https://matthewtran.dev/2022/12/jabican-usb-pro/), I decided to see how cheaply I could make a responder node. In the automotive industry, LIN is frequently used to control buttons and lights. Thus I did just that with my board. It’s quite a simple design with the most interesting part being using a NMOS to act as a level translator between the LIN line and the ATtiny10’s IO. It doesn’t have the same slope control or wake features more expensive LIN transceivers have, but it works quite well.

The firmware was also pretty straightforward with the oscilloscope helping a lot with checking my timing. While a more complex solution would have used interrupts and timers, I wanted to move quickly and stuck with polling. In order to use only one IO for LIN, I had to switch between input and output quickly (AVR doesn’t have open-drain mode). There’s not much more to say honestly; it really was a straightforward implementation.
