---
title: Zephyr LIN Driver
date: 2022-12-10
categories: projects
excerpt: Inspired by the CAN API, I designed a LIN API for Zephyr along with one implementation built on top of the UART driver.
header:
  teaser: /assets/img/2022/zephyr_lin.jpg
---

<https://github.com/dragonlock2/zephyrboards/blob/main/include/zephyrboards/drivers/lin.h>
<https://github.com/dragonlock2/zephyrboards/tree/main/drivers/lin>

After hearing about it for so long, I finally had an opportunity to work with LIN while working in industry. Designed as a low-cost alternative to CAN, it’s actually quite simple. Virtually any microcontroller with a UART can become a LIN node when coupled with a LIN transceiver. Given this, I decided to add LIN support into Zephyr.

## LIN protocol

At the physical layer, LIN is a bus-based architecture with all nodes sharing the same LIN line. The LIN transceiver translates UART signals to the voltage required by LIN with TX driving the bus as needed and RX acting as feedback. This is quite similar to what a CAN transceiver does. In fact, while impractical, one could in theory use the CAN physical layer for LIN with a transceiver swap.

At the link layer, LIN operates on a commander-responder architecture. The commander initiates a packet by sending a break, sync byte, and PID. Then it sends or waits for a payload and checksum response as needed. One interesting caveat I noticed was that LIN packets don’t contain their length. That means there’s a non-zero chance that a random long packet will get received as a shorter one simply because one of the data bytes was also a valid checksum. After playing with a PeakCAN device, I realized the solution was just to know how long the packets you want to receive are.

## Zephyr

Designing the LIN API for Zephyr was relatively straightforward with most of the methods mimicking the CAN API. Since it’s possible for some microcontrollers to have a LIN hardware block, it’s important that the LIN API support several possible underlying implementations.

With the LIN API done, I proceeded with an implementation using the Zephyr UART API. In order to be non-blocking, everything would have to be interrupt based. Couple that with supporting a packet timeout and making sure LIN API calls don’t affect in-flight packets and I had a big synchronization problem on my hands. I dealt with simultaneous LIN API and UART ISR calls by encapsulating all LIN operations in a lock. Since I can’t guarantee the priorities of the UART and timeout ISRs, I had to trace all code paths to make sure either one interrupting the other at any point wouldn’t cause any issues.

One interesting quirk of UART peripherals I found was that changing the baud rate meant that the next byte sent out would be delayed by at least one byte time. Since I had to change the baud rate in order to send a break, it meant that my LIN packets would just barely comply with the LIN spec.

A bug I found in both the STM32 and NXP UART drivers was that the error check function blindly clears errors bits that aren’t even set. Typically this would also clear a pending received byte. Thankfully, Zephyr’s build system makes it relatively easy to temporarily apply patches to fix this behavior.

At the end of the day, everything worked! It’s certainly not fully LIN spec compliant especially with the API the spec defines, but those layers should be buildable if it ever became necessary.

### 11-29-23 Update

Over a year later and with much more LIN experience, I revisited my LIN API. Since I tried too hard to match the CAN API, the underlying UART implementation consumed ~3.5KiB of RAM per instance which is ridiculous. Since LIN is such a slow protocol, there's no need to queue messages for sending like with USB. As such, I rewrote the API to be callback based so we can generate packets on the fly, significantly reducing memory usage. I also changed the timeout method from a single overall timeout to between individual bytes, greatly simplifying dealing with preemption issues between the UART interrupt handler and the timeout handler. It's not 100% LIN compliant, but works more than well enough.
