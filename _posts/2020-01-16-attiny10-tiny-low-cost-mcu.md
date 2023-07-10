---
title: ATtiny10 - Tiny, Low-Cost MCU
date: 2020-01-16
categories: cool-chips
excerpt: Curiosity about the cheapest Atmel MCU led to the ATtiny10. Despite what at first may seem like severe limitations, it's pretty capable.
header:
  teaser: /assets/img/2020/attiny10.jpg

gallery:
  - image_path: /assets/img/2020/pcb_7.jpg
  - image_path: /assets/img/2020/pcb_6.jpg
---

A couple years ago when I was placing my first order on Digi-Key, I wondered what the cheapest Atmel microcontroller there was. Turns out it was the ATtiny10 for about $0.35. This little microcontroller really packs quite the punch with 1KB of flash and an astounding 32 bytes of SRAM. It even has a single 16-bit timer with 2 PWM channels and a 4 channel 8 bit ADC. Including the reset pin, it has 4 I/O lines. Even more, it has an internal 8MHz oscillator. Despite its limitations people have done quite interesting things with these chips. One of the first things I noted when looking at this chip was that it had the perfect number of pins to control an RGB LED. Years later and wanting a really simple circuit to test out making double-sided PCBs, I decided to go through with the idea.

{% include gallery %}

The ATtiny10 uses a TPI programming interface. Not as cool as UPDI, but pretty cool nevertheless. In order to get a 3rd PWM pin, for fun I took the less conventional route of using an interrupt every time the timer overflowed to decide what to do with the 3rd pin. This way I could use the native PWM functionality of the other 2 pins. Surprisingly, I didn’t need to worry about using up too much SRAM at all because most of the code just did register operations.

{% include figure image_path="/assets/img/2020/attiny10.jpg" %}
