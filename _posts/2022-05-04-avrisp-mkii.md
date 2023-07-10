---
title: AVRISP MKII
date: 2022-05-04
categories: projects
excerpt: I might be a couple years late to the party, but here's a tiny board powered by LUFA's AVRISP MKII project.'
header:
  teaser: /assets/img/2022/avrispmkii.jpg
---

<https://github.com/dragonlock2/kicadboards/tree/main/projects/arvispmkii>

After using an AVRISP MKII created from an Arduino Uno for years, I decided to finally figure out where that custom firmware came from. Turns out it came from [LUFA](https://github.com/abcminiuser/lufa/tree/master/Projects/AVRISP-MKII). With that, I designed a board around it. I definitely didn’t want to buy new parts for this, so I used what I had. While the MPLAB Snap is preferred due to its wide protocol support, I will continue using the AVRISP MKII since it’s supported in Arduino IDE. After modifying the LUFA project a bit to match the clock speed, GPIO, and chip, I got it working! All of my programmers are now tiny and it’s beautiful.
