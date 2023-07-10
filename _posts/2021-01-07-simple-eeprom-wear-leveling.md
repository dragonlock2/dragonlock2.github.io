---
title: Simple EEPROM Wear Leveling
date: 2021-01-07
categories: projects how-to
excerpt: A one bit overhead wear leveling algorithm for storing fixed size data in EEPROM. Based on Danny Chouinard's work.
header:
  teaser: /assets/img/2021/wlprom.jpg
---

In order to deal with the limited write cycles on EEPROM, wear leveling algorithms are commonly used. Generally speaking, the most common use case is storing fixed size data like user settings. After some searching, I came across a really clever algorithm that uses only one extra bit on top of the stored data. It’s a solid read I’d recommend checking it out.

- <https://sites.google.com/site/dannychouinard/Home/atmel-avr-stuff/eeprom-longevity>

## Algorithm

Conceptually, we start by splitting the memory into evenly sized chunks that’s the size of the data we’d like to store plus one bit. Our goal is to write to a different chunk each time to spread out the writes. The extra bit, which we call a sentinel bit, is used to mark where the last written data is. We’ll write the sentinel bits in such a way that it’s a sequence of 1s followed by 0s or 0s followed by 1s.

Every time we want to read our data, we search for the location just before our bit changes which gives us the last written data. If the bit doesn’t change, it means the last index in our array of chunks is the last written data. Rather than searching linearly and comparing adjacent indices, we can use binary search and compare against the first index for that sweet O(log n) runtime.

Every time we want to write data, we simply write to the location after the last written data, keeping the same sentinel bit as the last written data. If we rollover, we flip the sentinel bit. This is how we maintain that the sentinel bit change marks our most recent data.

## Implementation

To test out the algorithm, I wrote it in C++ on Mbed. It interacts with a separate EEPROM library that provides a simple random byte-level read/write interface. My implementation when writing doesn’t read in the last written data to set the correct sentinel bit but rather assumes the passed in data has the correct sentinel bit. This has a slight performance improvement at the cost of needing to be careful not to modify the sentinel bit and having to read it in the first time before writing.

{% gist d97fd3b2cd98ce1b930640b9e46618cf %}

The EEPROM I tested on is the [BRCF016GWZ](https://fscdn.rohm.com/en/products/databook/datasheet/ic/memory/eeprom/brcf016gwz-3-e.pdf). I pretty much just wanted to try soldering a CSP package. It can only write a certain number of bytes at a time, so I had to convert that interface to one that can write any number of bytes.

{% gist c75fe401a6d6384656cea15f4d8a7f7a %}

## Extras

As a simple demonstration of this algorithm, the code works really well, but there’s definitely some features that could be added. We could add a CRC or checksum to detect errors and potentially fix them or revert to the last good write. Due to the nature of the algorithm, we also keep track of the past couple writes. Support for multiple instances or being able to split the memory up to write more than one kind of data could also be added. Even accounting for the memory itself and using a more optimized write pattern could be looked into.
