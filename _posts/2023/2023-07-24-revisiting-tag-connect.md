---
title: Revisiting Tag-Connect
date: 2023-07-24
categories: projects
excerpt: Recreating patented technology yet again but this time using OSH Park for the PCBs.
header:
  teaser: /assets/img/2023/tagconnect-3.jpg
---

<https://github.com/dragonlock2/kicadboards/tree/main/projects/tagconnect>

Like in my last [post](/2020/10/diy-tag-connect-cable/), the Tag-Connect technology is still patented for about another 10 years. What I'm doing is legally questionable but ethically not.

Since backups are important, I decided to design a version that can be sent to a normal PCB fab like OSH Park. Tolerancing the 1mm holes was the biggest worry but thankfully it turned out ok. Going a little bit tight turned out to be a benefit since it helped keep things super aligned. Since 2x3 1.27mm headers are hard to come by, I also used this as an opportunity to do my first flex PCB design and develop a standardized pinout I can use across all my future boards.

{% include figure image_path="/assets/img/2023/tagconnect-2.jpg" %}
{% include figure image_path="/assets/img/2023/tagconnect-1.jpg" %}
