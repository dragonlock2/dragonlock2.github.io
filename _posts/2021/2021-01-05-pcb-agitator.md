---
title: PCB Agitator
date: 2021-01-05
categories: projects
excerpt: This glorified camera slider halves my etch times and improves etching consistency all in an overkill but stylish form factor.
header:
  teaser: /assets/img/2021/agitator_19.jpg

gallery:
  - image_path: /assets/img/2021/agitator_12.jpg
  - image_path: /assets/img/2021/agitator_14.jpg
  - image_path: /assets/img/2021/agitator_15.jpg
  - image_path: /assets/img/2021/agitator_16.jpg

gallery2:
  - image_path: /assets/img/2021/agitator_7.jpg
  - image_path: /assets/img/2021/agitator_8.jpg
  - image_path: /assets/img/2021/agitator_9.jpg
  - image_path: /assets/img/2021/agitator_10.jpg
  - image_path: /assets/img/2021/agitator_11.jpg
  - image_path: /assets/img/2021/agitator_13.jpg
  - image_path: /assets/img/2021/agitator_17.jpg
  - image_path: /assets/img/2021/agitator_18.jpg

gallery3:
  - image_path: /assets/img/2021/agitator_4.jpg
  - image_path: /assets/img/2021/agitator_5.jpg
  - image_path: /assets/img/2021/agitator_6.jpg
---

One of the issues I was running into when etching PCBs was uneven etch rates and long etch times. The solution is to keep the etchant moving across the board, commonly known as agitation. While I could have just taped a vibration motor to my etching container, I decided to make something a bit fancier.

## Design

{% include figure image_path="/assets/img/2021/agitator_1.jpg" %}

As with most projects, the direction of my design was heavily dictated by the parts I had lying around. I went for a highly symmetric and clean design. Mechanically, it’s basically a camera slider. I wanted to implement some sort of closed loop control, so I added homing Hall effect sensors and a magnetic encoder similar to what I used in the [PCB Laminator](https://matthewtran.dev/2019/06/pcb-laminator/). The UI was trickier to implement since I wanted to use as few buttons as possible. To maximize flexibility, I still wanted to be able to set a start point, end point, acceleration, and max velocity. Seeing as I already had an encoder on the sliding mechanism, that became the slider to pick my settings. Pair it with one button and we are good to go.

## Electrical

The schematic was pretty straightforward. This was the first time I used an ATtiny1616 which is now my designated microcontroller for low power use cases. I even added input voltage monitoring because I have destroyed several LiPo packs from accidental over-discharge.

{% include figure image_path="/assets/img/2021/agitator_3.jpg" %}

The PCB layout was also pretty straightforward. Keeping up with the whole symmetry theme, I made it as symmetric as possible.

{% include figure image_path="/assets/img/2021/agitator_2.jpg" %}

As usual, the PCB came out pretty good.

{% include gallery %}

## Assembly

After several hours of 3D printing, CNC routing, and sanding, my parts were all ready for assembly.

{% include gallery id="gallery2" %}

Wanting a more integrated solution than using silicone oven mats to prevent the etching container from sliding around, I decided to cover the platform in hot glue. I tried using a heated bed for a 3D printer to smooth it out, but without a release agent it just made a mess. The end result isn’t smooth, but it’s got texture.

{% include gallery id="gallery3" %}

## Software

I developed the code using Atmel START and Atmel Studio. Getting the basics up and running was pretty easy but the control loop was where things got interesting. I started with an open loop system and after several iterations I settled on an Arduino [AccelStepper](https://www.airspayce.com/mikem/arduino/AccelStepper/) inspired algorithm. I had to switch to full stepping because the computation was too heavy so there’s definitely some optimizations to be made there.

Adding in the closed loop took a few iterations to get the behavior I liked. The resolution of the encoder is about 1mm, so it’s really only good enough to counter stalling. At first I tried incorporating the encoder data and restart the open loop trajectory upon stalling, but it just didn’t feel right. Eventually I settled upon what I like to call clopen loop control. Basically the encoder data is used only after finishing a full trajectory. If it stalls in the middle, it doesn’t care. Couple that with traveling to the farther endpoint each time and I had something that just felt right. It even stops moving when it runs into the homing sensors which is a plus.

There were a couple of other interesting bits like a custom variable microsecond level delay made by counting cycles, state machine, analog comparator interrupt, and more. I don’t think it’s good enough to throw on Github, so the full code can be downloaded [here](/assets/zip/Agitator.zip) as a zip.

## Demo

I have to say it works pretty well. It’s pretty surprising how much of a difference agitation makes to etching PCBs.

{% include video id="oFWEokCxA_s" provider="youtube" %}

{% include video id="WKkd1ORuvCs" provider="youtube" %}

{% include video id="vjOV97aMJiw" provider="youtube" %}

{% include video id="6LXCrswkLD8" provider="youtube" %}
