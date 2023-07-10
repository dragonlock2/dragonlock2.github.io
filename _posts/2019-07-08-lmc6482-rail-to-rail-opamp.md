---
title: LMC6482 - Rail to Rail OpAmp
date: 2019-07-08
categories: cool-chips
excerpt: An excellent opamp for prototyping.
header:
  teaser: /assets/img/2019/lmc6482.jpg

gallery:
  - image_path: /assets/img/2019/piezo-amplifier.jpg
  - image_path: /assets/img/2019/clamp-overview.jpg
---

<sub>Written 8-19-19</sub>

When I was just getting started using opamps late last year, I decided to buy a bunch of the most popular one, LM358. Little did I know about all the various specifications that I had to consider when picking the right opamp. At the time I was trying to amplify the signal for a sine wave encoder I was working on, but I hit a wall when the maximum voltage I could get out of the LM358 was around 3.7v with a 5v power input. It was then that I found out that I had to use a rail to rail opamp. Soon after though I was entering my senior year of high school, complete with a stressful college application season and engineering for upcoming SciOly 2018 competitions and team tryouts, so I set my tinkering aside for the time being.

Enter EE16B lab section during my 2nd semester at UC Berkeley. We used opamps pretty extensively in that class for various purposes but one of the things I noticed was that we used an [LMC6482](http://www.ti.com/product/LMC6482), which was a rail to rail opamp. We were also forced to order a free sample of them which was pretty awesome. So I spent plenty of time with this cool chip. For me the most important feature is its rail to rail output, but a lot of other specifications, from CMRR to input current are also excellent.

{% include gallery %}

It is a little expensive though compared to an LM358, but TI’s sample program is pretty generous to students.
