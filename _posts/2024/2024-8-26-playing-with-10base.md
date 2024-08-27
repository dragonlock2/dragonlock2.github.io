---
title: Playing with 10BASE-T1S and 10BASE-T1L
date: 2024-8-26
categories: projects
excerpt: Designed some boards and wrote an Open Alliance SPI driver to talk to the NCN26010 and ADIN1110 MAC-PHYs.
header:
  teaser: /assets/img/2024/playing_with_10base_1.webp

gallery:
  - image_path: /assets/img/2024/playing_with_10base_2.webp
  - image_path: /assets/img/2024/playing_with_10base_3.webp
---

[miscboards/nxp/lpc1549_oaspi](https://github.com/dragonlock2/miscboards/tree/main/nxp/lpc1549_oaspi)\
[kicadboards/breakouts/ncn26010_oaspi](https://github.com/dragonlock2/kicadboards/tree/main/breakouts/ncn26010_oaspi)\
[kicadboards/breakouts/adin1110_oaspi](https://github.com/dragonlock2/kicadboards/tree/main/breakouts/adin1110_oaspi)

Since microcontrollers with built-in MACs tend to be more expensive, external MAC-PHY chips can be used instead and talked to over SPI. Open Alliance SPI standardizes the communication protocol so that roughly the same driver can be used for any MAC-PHY. With sufficient CPU and SPI bandwidth, one can achieve the full 10Mbps of either 10BASE-T1S or 10BASE-T1L.

## hardware

I did a board design for each of 10BASE-T1S and 10BASE-T1L, using the NCN26010 and ADIN1110 MAC-PHYs respectively. The circuits for them are quite simple, I mainly just followed the datasheet and evaluation boards. For 10BASE-T1S, it's important to note that the end and drop nodes have different termination. The drop nodes don't need termination, but adding a little generally helps noise immunity. Since I had samples, I chose the LPC1549 as the microcontroller. The connection from the MAC-PHY to the microcontroller is like any SPI device (SDO, SDI, SCK, CS) with an added interrupt pin.

For the layout, there isn't much to say. I kept it pretty small and on two layers and was able to reuse much of the layout between boards since they were so similar. The switch matrix of the LPC1549 helped ease the layout since I could remap the SPI pins anywhere.

## firmware

Starting out, I got the LPC1549 SDK running similar to how I did for [lpc1768_poe](../../../2024/06/lpc1768_poe/). I ran into some issues where flashing once would end up with this one specific sector being empty. Flashing twice fixed it. Correctly setting the CRP helped significantly. Interestingly, the LPC1768 has the same CRP but I had no issues with it. This might be because the LPC1549 has a substantial bootloader in its boot ROM. Overall, the SDK was quite nice to use. I ran into some issues with a SPI DMA driver, but I got it working eventually. TinyUSB and FreeRTOS setup was smooth sailing as always to set up since it's already supported.

For the Open Alliance SPI (OASPI) driver, I started by implementing control transfers which is how we interact with registers. For reliability, control transfers have a parity bit and send/receive the inverse of the data payload. For simplicity, I just retried the transfer until no errors were detected. The configuration for the NCN26010 and ADIN1110 are quite different with regards to the MAC filtering and PHY registers, but it's overall quite similar. Next, I implemented data transfers. While it may not be the most portable, using bitfields was nice to parse out the packet fields. Data transfers use a parity bit to protect the header like with control transfers. To protect the data itself, the normal FCS of Ethernet frames is used, preferably for both TX and RX. I added a helper for that.

For connecting to an Ethernet stack, the exact implementation can vary. I wanted to make a USB converter so used the TinyUSB API which boils down to a function to send a packet and one to receive one. I started with a high priority thread that busy looped looking for and assembling received packets. Then I added the interrupt pin so the thread could sleep until RX data was available. After that, I added the ability to send packets which was a similar process to receiving packets and was sent on the same bidirectional data transfers. The thread would now only sleep if no RX data was available, no TX buffer space was available, and no TX packets are queued. The way OASPI defines interrupt triggers helps make sure the driver only performs data transfers when needed. In all of this, I also made sure to check for errors and just drop packets if I got any.

In terms of performance, the driver works pretty well. Measuring on an oscilloscope, the effective bandwidth is around 12Mbps if packets are aligned to chunk boundaries and roughly half that if not. About half the time is spent sleeping waiting for SPI to finish. Another quarter is the CPU processing and checking the packet data. The last quarter is FreeRTOS task switching overhead which I could potentially reduce by setting up longer SPI transfers at the cost of latency and memory. For reference, this is a 72MHz Cortex-M3 with some flash latency.

In the future, it would be good to buffer the packets going to and coming from TinyUSB. I'm definitely losing some packets if the OS doesn't read fast enough. It would be fun to play with cut-through mode for OASPI, squeezing a TCP/IP stack on, PoDL for 10BASE-T1S, topology discovery, and IEEE 1588 hardware timestamping. For now, this was a successful exploration.

{% include gallery %}