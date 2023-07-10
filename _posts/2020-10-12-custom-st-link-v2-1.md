---
title: Custom ST-Link V2-1
date: 2020-10-12
categories: projects
excerpt: After my ST-Link V2 clone broke, I scoured the web for a way to build one from scratch. I ended up with a custom ST-Link with built-in UART VCP.
header:
  teaser: /assets/img/2020/stlinkv2_11.jpg

gallery:
  - image_path: /assets/img/2020/stlinkv2_2.jpg
  - image_path: /assets/img/2020/stlinkv2_3.jpg
  - image_path: /assets/img/2020/stlinkv2_4.jpg
  - image_path: /assets/img/2020/stlinkv2_5.jpg
  - image_path: /assets/img/2020/stlinkv2_6.jpg
  - image_path: /assets/img/2020/stlinkv2_7.jpg
  - image_path: /assets/img/2020/stlinkv2_8.jpg

gallery2:
  - image_path: /assets/img/2020/stlinkv2_9.jpg
  - image_path: /assets/img/2020/stlinkv2_10.jpg
  - image_path: /assets/img/2020/stlinkv2_11.jpg
  - image_path: /assets/img/2020/stlinkv2_12.jpg
---

After my ST-Link V2 that I bought from Amazon decided to break at the worst time, I decided to look into building my own programmers. Much like how I built an [AVRISP mkII](https://make.kosakalab.com/make/electronic-work/avrisp-mk2/uno-r3_avrisp-mk2_en/), I wanted to do the same for STM32. Looking around the web for a bit, I found out that it’s actually possible to create an ST-Link V2-1 (which has a VCP!) completely from scratch because someone managed to download the firmware from secure flash. I certainly don’t trust installing software I just find randomly online so I ran it in a VM to hopefully be safe. To my surprise, it worked. It’s even updatable through the normal ST-Link update utility.

{% include figure image_path="/assets/img/2020/stlinkv2_1.jpg" %}

As with any project, I had to turn it into a PCB. I based the design off a Nucleo schematic.

{% include gallery %}

Once the DIY PCB route worked, I decided this would be the programmer I’d use for UR@B which I’d affectionately name NOGPROG. I recently heard of OSH Park so I gave them a try. Definitely impressive quality and service. As always, I took great pride in making 3D-printed cases to cover up my imperfect soldering.

{% include gallery id="gallery2" %}

Was the LQFP package out of stock the first time around? Yes that’s why I used a QFN one instead. Did I accidentally buy the AZ1117CR2 instead of the AZ1117CR at first? Yes that’s why one of them doesn’t look like the others. Did I buy the wrong crystal the second time? Yes that’s why the soldering is a little janky from the Kapton tape I put underneath.

Next up I have to figure out how someone could pull the firmware off a secured chip. It looks like lujji was the one who figured out a clever way pull the bootloader. I’ll try to follow their work one day and make step by step instructions but for now it’s just more worth my time to buy an ST-Link V3.

## Resources

- <https://sudonull.com/post/32259-Making-ST-Link-V21-from-Chinese-ST-Link-V2>
- <https://lujji.github.io/blog/reverse-engineering-stlink-firmware/>
