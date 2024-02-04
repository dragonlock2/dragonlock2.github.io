---
title: PCB Reflow Oven
date: 2018-01-07
categories: projects
excerpt: Repurposing a toaster oven that's older than I am to help out with reflow soldering.
header:
  teaser: /assets/img/2018/reflow-done.jpg

gallery:
  - image_path: /assets/img/2018/reflow-done.jpg
  - image_path: /assets/img/2018/reflow-innards.jpg
---

<sub>Written 8-29-19</sub>

One of the tools that I learned about while diving into SMD was a reflow oven. It’s basically a programmable oven that’s useful for soldering because it can bring a board through the optimal temperature curve. Moreover, I would also end up using it for properly desoldering components and trying to anneal 3D printed parts.

After we bought a new toaster oven, I was finally free to use the old one for my own project. Taking it apart, I admired the 20 year old construction that still worked perfectly even to this day. Well, I actually gutted the machine so technically the old electronics are not working anymore.

{% include figure image_path="/assets/img/2018/reflow-teardown.jpg" %}

## Hardware

Surprisingly, I didn’t really take any pictures of my build process, so I’ll just describe some of the main things I considered while building the reflow oven.

First, I needed to figure out how to mount the thermocouple. Since the oven would probably get up to around 250°C, that ruled out pretty much any plastic I had easy access to. I also didn’t know about Kapton tape at the time. Rummaging through my metal parts bin, I eventually had the idea of using a piece of an aluminum arrow to extend into the oven chamber. To mount it to the sheet metal chassis of the oven, I used a die to thread one end and two nuts on opposing sides to hold it in place.

{% include figure image_path="/assets/img/2018/reflow-thermocouple.jpg" %}

Next was the electronics. I took a zero crossing detector design I found online in order to help do PWM control of the AC voltage later. Since the oven was rated at about 1500W, I used two TRIACs, one for each heating element. Of course, I used some optoisolators to connect them to the microcontroller. At the time the Atmega328P-PU was my goto chip so I used it. Lastly, I used an Apple USB charger to power the all of the 5v logic.

For a user interface, I decided to use a standard 16×2 LCD module along with some metal switches I got from Adafruit. What’s pretty cool is that I machined the cutout for the LCD using my CNC mill which I operated remotely by hand. The thermoset used in the oven was very fun to machine.

After soldering all the components to a perfboard and fitting everything into the side panel of the oven, I ended up with this.

{% include gallery %}

## Software

With the hardware functional, I started writing the code. The first step was controlling the heating elements to achieve a target temperature. Although I hooked up both heating elements separately, in the code I considered them as one because maintaining an even chamber temperature needed multiple thermocouples. Since I was using a zero crossing detector, I tried implementing AC phase control to control the heaters. It didn’t work particularly well, so I switched to just letting a certain percentage of half waves pass. Heaters have a slow response time so this method is ok. After figuring out how to control the heaters, I added a PID loop to finish it up. Tuning that loop, however, was another challenge altogether, but after a lot of trial and error I got a respectable response time and overshoot.

Next up was the user interface. This was the most time consuming part of the entire project. I didn’t really know about structs, so I used multiple 2D arrays to store the profiles. Also, I could’ve moved a lot of code to a separate file to make everything cleaner. Still, I ended up with a working product that has a relatively simple user interface. I made adding custom profiles relatively straightforward and made sure to support ramping and waiting to reach a target temp.

My code can be found [here](https://gist.github.com/dragonlock2/6ffff3bab0b6ffeb1ea236e82348d606).

The oven ended up working perfectly! You can see its use in some of my later posts.
