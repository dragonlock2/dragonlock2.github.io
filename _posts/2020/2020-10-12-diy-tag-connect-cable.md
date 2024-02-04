---
title: DIY Tag-Connect Cable
date: 2020-10-12
categories: projects
excerpt: While browsing through KiCad, I learned about the clever Tag-Connect system. Given the high cost, I decided to replicate the design for myself.
header:
  teaser: /assets/img/2020/tagconn_8.jpg

gallery:
  - image_path: /assets/img/2020/tagconn_1.jpg
  - image_path: /assets/img/2020/tagconn_2.jpg
  - image_path: /assets/img/2020/tagconn_6.jpg
  - image_path: /assets/img/2020/tagconn_4.jpg
  - image_path: /assets/img/2020/tagconn_3.jpg
  - image_path: /assets/img/2020/tagconn_5.jpg
  - image_path: /assets/img/2020/tagconn_23.jpg

gallery2:
  - image_path: /assets/img/2020/tagconn_17.jpg
  - image_path: /assets/img/2020/tagconn_18.jpg
  - image_path: /assets/img/2020/tagconn_19.jpg
  - image_path: /assets/img/2020/tagconn_20.jpg
  - image_path: /assets/img/2020/tagconn_21.jpg
  - image_path: /assets/img/2020/tagconn_22.jpg
  - image_path: /assets/img/2020/tagconn_15.jpg
  - image_path: /assets/img/2020/tagconn_16.jpg

gallery3:
  - image_path: /assets/img/2020/tagconn_7.jpg
  - image_path: /assets/img/2020/tagconn_9.jpg
  - image_path: /assets/img/2020/tagconn_10.jpg
  - image_path: /assets/img/2020/tagconn_11.jpg
  - image_path: /assets/img/2020/tagconn_12.jpg
  - image_path: /assets/img/2020/tagconn_13.jpg
---

**Disclaimer:** The original design is [patented](https://patents.google.com/patent/US8057248B1/en?inventor=Neil+S.+Sherman). This post is meant as a purely educational exploration into the manufacturing process of a clever invention. By no means should my method be used in any commercial capacity. Even personal use is of questionable legality. Please support the original inventor.

While looking through KiCad footprints, I came across the curious Tag-Connect ones. Upon further research, I found out they were an extremely clever alternative to bulky and expensive programming headers on PCBs. However, each cable costs around $40. The basic concept was rather simple, so I figured I’d try my hand at making one.

The basic design involves using two PCBs to maintain the proper spacing between the pogo pins. Since I needed maximum accuracy, I dusted off my CNC router which I hadn’t used in probably a year.

{% include gallery %}

After building my custom [ST-Link V2-1’s](https://matthewtran.dev/2020/10/custom-st-link-v2-1/), I decided to build a slimmer one. I’d also use an unbroken 1.0mm drill bit this time.

{% include gallery id="gallery2" %}

I even built a 6-pin one for AVR programming. I also use it for SWD when I don’t need the UART.

{% include gallery id="gallery3" %}

Over the summer, I was able to get my hands on a legitimate Tag-Connect cable to do a comparison. The real thing is much bulkier but of higher quality, precision, and durability. It uses ~0.9mm rods instead of 1.0mm and has better pogo pins with what I believe are crown heads. For $2 in materials but an absurd 2 hour manufacturing time, I’d say this was a pretty successful project but not worth doing for the average maker.
