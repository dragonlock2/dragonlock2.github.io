---
title: Embedded 3D Printed Hidden QR Code
date: 2018-04-06
categories: projects other
excerpt: Instead of studying for a math test, I spent a week coming up with the nerdiest promposal I could.
header:
  teaser: /assets/img/2018/promposal-two.jpg

gallery:
  - image_path: /assets/img/2018/promposal-light.jpg
  - image_path: /assets/img/2018/promposal-two.jpg
---

<sub>Written 8-30-19</sub>

During the latter half of my senior year of high school with senioritis kicking in hard, I decided to spend a week figuring out a promposal. I could have been stereotypical and made a poster, but that’s not my personality. I also could’ve been studying for a math test coming up, but who needs to study anyway? At first, I wanted to try making a POV display using my broken v1 lightsaber and spinning it by hand, but that proved a little hard to see on camera. Talking to my friend about puzzles, I had the idea of using a QR code. Of course, I couldn’t just print it out on paper. Since I was making a puzzle, it made sense to make finding the QR code a puzzle too.

First I had to figure out how robust a QR code was. There’s redundancy so a good portion of the code can be damaged but still be readable. Also, the colors can be inverted and the whole code rotated and it’ll still read. Moreover, colors don’t matter much they just have to have a good contrast with each other. The most important factor I had to account for ended up being contrast.

Initially my idea for embedding a QR code in a credit card form factor was to print two layers, paint the QR side black, and then glue them together. This didn’t work well and wasn’t durable. Then I tried getting everything to work in one print. After a couple test prints and optimizations, I ended up with a QR code of acceptable quality embedded. The top and bottom are solid, but there’s air gaps in the middle that represent the QR code.

{% include figure image_path="/assets/img/2018/promposal-cad-1.jpg" %}

Scanning the QR code reliably was another issue I had to deal with. When looking from an angle or even straight on if it’s dark enough, the QR code is not noticeable. However, when I shined light through it, the QR code appears. Because the contrast isn’t quite high enough, it’s hard to scan with a standard QR code scanner. After much trial and error, I found out that if you put the card against a bright light, take a picture, and crank the contrast to the maximum, then the picture is scannable. Sometimes if the light is particularly bright, such as in sunlight, the card is scannable normally.

{% include gallery %}
