---
title: CS61C - Computer Architecture
date: 2019-12-11
categories: school
excerpt: A course with a bit of an information overload about the big ideas of computer architecture that ended up being one of my favorite courses.
header:
  teaser: /assets/img/2019/61c_mbothighres.jpg

gallery:
  - image_path: /assets/img/2019/61c_mbot0.jpg
  - image_path: /assets/img/2019/61c_mbot1.jpg
  - image_path: /assets/img/2019/61c_mbot2.jpg

gallery2:
  - image_path: /assets/img/2019/61c_class0.jpg
  - image_path: /assets/img/2019/61c_class1.jpg
  - image_path: /assets/img/2019/61c_class2.jpg
  - image_path: /assets/img/2019/61c_class3.jpg
  - image_path: /assets/img/2019/61c_class4.jpg
  - image_path: /assets/img/2019/61c_class5.jpg
  - image_path: /assets/img/2019/61c_class6.jpg
---

This was easily one of my favorite courses because it operates right at the intersection of EE and CS. I really liked the focus on hardware, performance, and how things are actually implemented in real life. Even more, I learned about a wealth of technical challenges and solutions that I didn’t know much about before. Keeping in line with my love of embedded systems type projects, I was ecstatic at finally getting to learn C, RISC-V assembly, GDB, and Valgrind. In reality, the course focused more on the big ideas side and the coding part was mostly self-taught, but it was awesome nevertheless. Anyways, here’s a couple of projects we did.

## Mandelbrot

{% include gallery %}

We generated pretty mathematical images using C. This project served as a nice dive into C and memory management. Overall, it was a very straightforward project and I really liked how I felt that I knew almost exactly what the computer was doing behind the scenes.

After we learned about OpenMP and SIMD, we had a lab on vastly improving the performance of Mandelbrot because it’s an “embarrassingly parallel” task. To simplify things, we only had to determine if a point was in the set or not. I ended up getting a 31x speedup over the serial version, which really opened my eyes to how much multithreading and other parallel techniques can improve performance.

## CS61Classify

{% include gallery id="gallery2" %}

Our next project was to implement an Artificial Neural Net (ANN) to identify numbers from the MNIST dataset. This definitely sounds more impressive than it actually was. All we did was write a couple functions to do dot products and matrix multiplication. The details of training and running the actual neural net were all handled for us. The real challenge was doing it all in RISC-V assembly. It was quite fun and gave me a better understanding of how a higher level language like C can get directly translated into machine code.

## CPU

{% include figure image_path="/assets/img/2019/61c_cpu.jpg" %}

Last but not least, we implemented the logic for a RISC-V processor in Logisim. We made everything from the ALU to the immediate generator to the control logic. When it came time to put it all together, I started by organizing all the parts into the same format as the picture of the data path from lecture. Keeping everything neat, organized, and aesthetic is kind of my thing. Then I added everything else.

One interesting part of the project was the extra credit for the ALU. We had to implement the mulh instruction which gets the upper 32 bits from multiplying two 32 bit numbers. There’s no built-in Logisim block for this, so I did some algebra to figure out how to do it. A bit messy, but it worked perfectly.

The most tedious part of the project was the control logic. We had to provide the correct control signals for each part of the data path to support each instruction. I started by making a spreadsheet for each instruction and the control signals necessary. Then I spent a good 6 hours looking at each and every control signal and what parts of the inputs determine them. The number of times I said “uniquely determine” is countless. As far as I know, it was a slightly unorthodox approach, but very compact and clean. Well worth the headache.
