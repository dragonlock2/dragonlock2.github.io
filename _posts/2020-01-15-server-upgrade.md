---
title: Server Upgrade!
date: 2020-01-15
categories: projects
excerpt: I started off my winter break by finally upgrading the Pi 3 that had been powering my website to a proper x86-64 server.
header:
  teaser: /assets/img/2020/server_1.jpg

gallery:
  - image_path: /assets/img/2020/server_1.jpg
  - image_path: /assets/img/2020/server_2.jpg
  - image_path: /assets/img/2020/server_4.jpg
  - image_path: /assets/img/2020/server_5.jpg
  - image_path: /assets/img/2020/server_6.jpg
  - image_path: /assets/img/2020/server_7.jpg
  - image_path: /assets/img/2020/server_3.jpg
---

To kick off the start of my winter break, I finally replaced the Raspberry Pi 3 that had been powering my website for the last couple months with a proper x86-64 server. The Pi 3 was simply too slow to complete basic tasks on a WordPress site with reasonable speed.

The main thing I considered when speccing out the server was the cost of upkeep. Once hosting a website gets to about $10 a month it starts to become more economical to find a third party host. The Pi 3 very conservatively draws about 5W continuously, which running 24/7 puts it at about $6 a year to run. So a sub-50W draw was roughly what I was aiming for.

Initially I looked into old Xeon processors which are dirt cheap, but I’d be trading price for higher energy consumption. Then I considered buying a refurbished Dell PC, which did have its merits. At the end of the day, I decided to splurge a little and buy all new components, centering around an ASRock DeskMini A300 and Ryzen 3 3200G. Native support for NVME drives which I’ve been hearing about for so long was the cherry on top. After ordering everything on Black Friday and surviving finals week, I was finally able to put the computer together.

{% include gallery %}

Measuring the power draw when idle puts it at about 15W, which is about $18 a year to run. Not too shabby. Considering my website doesn’t get that many visitors, it’ll be running idle a great deal of the time. Even pinning one core to a 100% put power draw at about 30W. Despite the initial ~$350 investment, this server was well worth it. And it’ll provide something to tinker around with when I’m bored.

Backing up the site takes seconds instead of minutes. Experimenting with new themes and settings is no longer such a chore. Saving a post happens just like that. I can actually watch images being uploaded in real time. The performance difference is absolutely beautiful.
