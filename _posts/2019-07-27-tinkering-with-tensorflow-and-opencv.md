---
title: Tinkering with TensorFlow (and OpenCV)
date: 2019-07-27
categories: projects
excerpt: Some free time and a project idea provided the perfect opportunity to get my feet wet with TensorFlow and OpenCV.
header:
  teaser: /assets/img/2019/tf-imgs.jpg
---

<sub>Written 8-19-19</sub>

One project I’ve really wanted to do for a long time is a robot that identifies lightsabers and shoots at them using Nerf darts or something. Star Wars was a huge part of my childhood and recreating those iconic blaster deflection scenes would be so cool. I keep getting distracted by other cool things I want to do so hopefully I’ll get around to it next summer or so.

During my family trip to Maui this summer, I had a bunch of free time on my hands whenever we weren’t hiking, eating, or going to the beach. I thought about how I could be productive and settled on figuring out the vision system for my future robot.

A few weeks previously, I experimented with OpenCV on my Raspberry Pi 2 and tried using filters and other functions to draw a box around any identified lightsabers. It worked rather well, but it was prone to several inaccuracies that I couldn’t quite adjust out. It also didn’t work for flashlight sabers (like SaberForge), whose brightness decrease significantly by the end of the blade.

{% include video id="Uj7dXJSIqWI" provider="youtube" %}

My code also only worked for one lightsaber and didn’t identify any colors, so I decided that it was the perfect time to dive into using machine learning and object detectors to do what I wanted. I learned about using object detectors with OpenCV’s DNN module so I looked up how to train my own model. I decided on using TensorFlow because it’s really popular and there’s a lot of tutorials out there on it.

### Training a Model

If you want step by step instructions on how to train your own object detector using TensorFlow, check out some of the links below, especially the Medium articles. I will just be outlining the basic steps I took and fixes for some hiccups along the way.

The first part is choosing a model. Since I’m going to end up deploying my model on relatively weak hardware (probably a Jetson Nano when I eventually buy one) and lightsabers are pretty easy to describe and supposedly detect, I chose to use SSDLite MobileNet v2.

The next step is creating a dataset, which takes up a surprising amount of time. I spent quite awhile pouring through Google Images, picking out images of varying color, background, orientation, brightness. Since I wanted the model to work with flashlight lightsabers and not just LED blade ones, I made sure to also include a bunch of cosplay pictures.

{% include figure image_path="/assets/img/2019/tf-imgs.jpg" %}

After getting a bunch of images (all PNGs and JPEGs), I had to manually annotate each one. I used [LabelImg](https://github.com/tzutalin/labelImg) because it seemed to be the most popular and was quite easy to use. I put all of the generated XML files into a separate folder.

TensorFlow requires data to be in the TFRecord file format. There’s scripts that automatically convert the files from LabelImg to TFRecord, but I had issues with it and ended up writing my own script based off of the example on the Github. You can find it [here](https://gist.github.com/dragonlock2/f2486feb42fa211708a53ec85e45a74b).

Finally, I got onto doing the actual training. A lot of tutorials say to use train.py but the new way is using model_main.py. The [Github](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/running_locally.md) provides pretty clear directions on this. I then used TensorBoard to monitor everything.

{% include figure image_path="/assets/img/2019/tensorboard-light.jpg" %}

Since I was in Maui and didn’t have access to my GTX 970 powered desktop at home, I had to do all the training on my Macbook Pro. After 3 days of my Macbook running at basically 100% load, the training finally got to a point where I was happy with the accuracy. One thing to keep in mind is not to leave the training going on too long because you might end up overfitting.

Next is exporting the model as a .pb file for OpenCV. OpenCV also requires a .pbtxt to import which can be generated using tf_text_graph_ssd.py on the OpenCV repository. I ran into an AssertionError when running it, which I found a fix for [here](https://github.com/opencv/opencv/issues/11560). Turns out the nodes need to be sorted.

After all that, I was finally able to import my model into OpenCV and run it.

{% include video id="xziQ5t213Mg" provider="youtube" %}

The results are actually pretty good. My training data could have been improved to include multiple lightsabers hitting each other, but it did a great job nevertheless. One thing to note is that the video is slowed down because my Macbook isn’t quite fast enough to run the detector at the playback speed. Still, I’d call this a success.

Using TensorFlow to train and deploy models is pretty cool, but it doesn’t really teach you anything about how machine learning and object detectors actually work. I’m familiar with the basics, but I’m definitely going to take machine learning classes later because I really want to gain a fundamental understanding of how it works.

#### Sources:

- <https://medium.com/@WuStangDan/step-by-step-tensorflow-object-detection-api-tutorial-part-1-selecting-a-model-a02b6aabe39e>
- <https://towardsdatascience.com/creating-your-own-object-detector-ad69dda69c85>
- <https://towardsdatascience.com/how-to-train-your-own-object-detector-with-tensorflows-object-detector-api-bec72ecfe1d9>
- <https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/installation.md>
- <https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/running_locally.md>
- <https://jeanvitor.com/tensorflow-object-detecion-opencv/>
- <https://github.com/opencv/opencv/issues/11560>
- <https://www.pyimagesearch.com/2017/09/18/real-time-object-detection-with-deep-learning-and-opencv/>
