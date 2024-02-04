---
title: Pi Zero Gameboy
date: 2018-07-23
categories: projects
excerpt: A functional and fun Pi Zero powered Gameboy to relive some nostalgic memories.
header:
  teaser: /assets/img/2018/pi0gameboy-4.jpg

gallery:
  - image_path: /assets/img/2018/pi0gameboy-2.jpg
  - image_path: /assets/img/2018/pi0gameboy-3.jpg
  - image_path: /assets/img/2018/pi0gameboy-4.jpg
  - image_path: /assets/img/2018/pi0gameboy-1.jpg
---

<sub>Written 8-27-19</sub>

Among the many projects for the Pi Zero is a handheld retro gaming console. It was the perfect opportunity to use up the Pi Zero v1.2 (one without the camera connector) that I had in my parts bin. I also had a backup LCD for cars that from my testing was pretty much only useful as a game console display and not any kind of text. With some parts in mind to determine the form factor, I got to designing in Fusion 360.

{% include figure image_path="/assets/img/2018/pi0gameboy-cad.jpg" %}

After printing the parts out, I got to the electronics. I started with soldering the buttons onto some perfboard and drilling the right holes to fit into my design. Then I built a little low battery circuit which if I remember correctly used a couple of transistors. After that I glued the speaker in place along with the Pi Zero, LCD, and battery. Then I soldered wires from each button to the Pi, following the wiring diagram of the PiGRRL Zero.

One issue I ran into was the fact that I didn’t have a 5v boost circuit to power the Pi off a Li-ion. Since I didn’t really have time to wait for the part to come in, I decided to try powering the Pi’s 5v line directly off the Li-ion. To my surprise, it actually worked perfectly. The USB flash drive, keyboard, mouse, and LCD all worked just fine. While my method is usable, I would definitely just buy a boost circuit in the future to be sure of the long term reliability.

Finally, I installed the software which was a really straightforward process. I just followed the instructions on [Adafruit’s PiGRRL Zero](https://learn.adafruit.com/pigrrl-zero/overview). Audio isn’t enabled by default, so I followed [Adafruit’s Pi Zero PWM Audio](https://learn.adafruit.com/adding-basic-audio-ouput-to-raspberry-pi-zero/pi-zero-pwm-audio) instructions.

{% include gallery %}

At the end of the day, I had a functional and fun Pi Zero Gameboy. The Gameboy was the oldest console I ever had, so I get the most nostalgia playing games from that era.
