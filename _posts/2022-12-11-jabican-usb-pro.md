---
title: JABICAN-USB Pro
date: 2022-12-11
categories: projects
excerpt: Designed as an open-source alternative to the PCAN-USB Pro, JABICAN-USB Pro runs JABI to provide isolated CAN and LIN access over USB.
header:
  teaser: /assets/img/2022/jabican_usb_pro.jpg
---

<https://github.com/dragonlock2/kicadboards/tree/main/projects/JABICAN-USB%20Pro>

After using the PCAN-USB Pro FD at work, I decided to build an open-source competitor to it. The PCAN-USB Pro FD costs over $500 which is certainly inaccessible to most hobbyists. Drawing from the software stack I built with [JABI](https://matthewtran.dev/2022/07/jabi-just-another-bridge-interface/), I simply needed to design hardware to take advantage of it. It costs over $50 and lacks USB HS and CAN FD support, but that’s mainly due to me trying to only use parts I had on hand.

The hardware design was pretty straightforward with the new challenge being the isolation. I was finally able to use the isolated CAN transceiver I got samples of awhile ago. It includes an auxiliary IO pin which was used to implement the switchable 5V CAN rail the PCAN-USB Pro has. I wanted to one-up the PCAN-USB Pro and added an isolated 12V LIN rail. It also has a switchable 1kΩ pull-up on the LIN line for LIN commander mode.

The firmware was absolute hell to get running fully. The MK22FN1M0AVLH12 I chose was a more featured version of the one supported by Zephyr which meant a lot of debugging to figure out exactly where they were different. I nearly gave up while getting USB running after checking everything from the register map and clocks to probing the USB data lines. In my final try, I did some googling and found that the enabled-by-default MPU was the issue. Adding CAN support was more straightforward and involved copying feature definition code over, connecting interrupts correctly, and setting up clocks.

At the end of the day, once the low-level Zephyr board support was finished, getting JABI up and running was easy. I still have to add GUI support to JABI for it to truly compete with the PCAN-USB Pro, but the majority of the work is done.
