---
title: Pi Zero W USB Dongle
date: 2018-08-10
categories: projects
excerpt: All the power, convenience, and GPIO of a Raspberry Pi in the compact form factor of a USB stick.
header:
  teaser: /assets/img/2018/pi0w-dongle-capped.jpg

gallery:
  - image_path: /assets/img/2018/pi0w-dongle-capped.jpg
  - image_path: /assets/img/2018/pi0w-dongle-uncapped.jpg
---

<sub>Written 8-27-19</sub>

Among all the really cool things that a Pi Zero W can do is turning into a USB dongle. Power is provided over USB and the Pi shares your computer’s internet connection. All the power, convenience, and GPIO of a Raspberry Pi in a little USB stick.

The software setup of enabling USB dongle mode on a Pi is pretty trivial, but I’ll give all the steps I took to get the Pi up and running.

- Install the latest version of Raspbian (I use Etcher)
- Enable SSH (`touch ssh` in the boot directory)
- Enable USB mode
    - Open config.txt and add `dtoverlay=dwc2` to the very bottom
    - Open cmdline.txt and add `modules-load=dwc2,g_ether` after `rootwait`
- Plug the Pi into your computer (you can actually just connect a microUSB cable from the USB port on the Pi for testing purposes)
- SSH into it at raspberrypi.local and change the hostname in raspi-config to whatever you like
- Expand the file system in raspi-config
- Install Vim
- `sudo apt update && sudo apt upgrade`

In order to do that last command you’ll need to share your internet connection with the Pi. I recommend checking out this [site](http://www.circuitbasics.com/raspberry-pi-zero-ethernet-gadget/) for more info. If you’re on Windows and internet sharing isn’t working, bridging the ethernet connections is inconvenient but usable. MacOS is much simpler, just enable one setting.

With the software set up, I proceeded to work on a case. Firing up Fusion 360, I got to modeling.

{% include figure image_path="/assets/img/2018/pi0w-dongle-cad.jpg" %}

After printing it and lots of sanding to get every edge smooth, I had this.

{% include gallery %}

One thing I really liked about my 3D print is the fit of the cap. Inspired by the feel of a Patriot USB flash drive I had laying around, I eyeballed a couple of bumps on the cap. To my surprise, in one try I ended up with a cap that has a very satisfying slide and tactile click.
