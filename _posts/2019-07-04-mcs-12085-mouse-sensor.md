---
title: MCS-12085 - Mouse Sensor
date: 2019-07-04
categories: cool-chips
excerpt: A pretty cool sensor salvaged from a really old mouse.
header:
  teaser: /assets/img/2019/mcs12085-bottom.jpg

gallery:
  - image_path: /assets/img/2019/mcs12085-top.jpg
  - image_path: /assets/img/2019/mcs12085-bottom.jpg
---

<sub>Written 8-19-19</sub>

During one of my random thoughts, I had the idea of taking apart a mouse and reverse engineering its sensor for use with an Arduino. Rummaging through my dad’s old electronics, I found a PS2 mouse that I was pretty sure we would never use. First I used a PS2 library to communicate with the mouse and make sure it was still working. After that I took it apart to take a look at its sensor.

As it turns out, this mouse (I think it was a Dell) used a MCS-12085. It’s so old that I couldn’t find any major electronics distributors selling it. Surprisingly though, there are a bunch of articles online about this sensor. I proceeded to desolder this sensor and its associated components to put together my own board.

{% include gallery %}

While there were libraries available, the communication method shown in [datasheet](http://www.rmrsystems.co.uk/download/MCS12085.pdf) looked pretty simple so I decided it was the perfect exercise to do. I looked at code from this [library](https://github.com/jgrahamc/mcs12085) for inspiration.

{% highlight C %}
#define CLK_PIN 11
#define DAT_PIN 12

void setup() {
  Serial.begin(115200);
  mcs12085_init();
}

int x, y = 0;
void loop() {
  x += mcs12085_dx();
  y += mcs12085_dy();
  Serial.print(x);
  Serial.print(" ");
  Serial.println(y);
  delay(5);
}

void mcs12085_init() {
  pinMode(CLK_PIN, OUTPUT);
  pinMode(DAT_PIN, OUTPUT);
  digitalWrite(CLK_PIN, HIGH);
  digitalWrite(DAT_PIN, LOW);
  delay(100); //Power Supply Rise Time
}

int8_t mcs12085_dx() {
  return mcs12085_read_register(0x03);
}

int8_t mcs12085_dy() {
  return mcs12085_read_register(0x02);
}

uint8_t mcs12085_read_register(uint8_t reg) {
  mcs12085_write_byte(reg);
  delayMicroseconds(100);
  return mcs12085_read_byte();
}

uint8_t mcs12085_read_byte() {
  pinMode(DAT_PIN, INPUT);
  uint8_t result = 0;
  for (int i = 0; i < 8; i++) {
    digitalWrite(CLK_PIN, LOW);
    digitalWrite(CLK_PIN, HIGH);
    result = result << 1 | digitalRead(DAT_PIN);
  }
  pinMode(DAT_PIN, OUTPUT);
  return result;
}

void mcs12085_write_byte(uint8_t val) {
  for (int i = 0; i < 8; i++) {
    digitalWrite(CLK_PIN, LOW);
    digitalWrite(DAT_PIN, val & 1 << 7); //get msb
    val = val << 1;
    digitalWrite(CLK_PIN, HIGH);
  }
}
{% endhighlight %}

The sensor actually worked really well. I’ll probably use it for some kind of robot in the future but for now it’s nice to add another sensor to my repertoire.
