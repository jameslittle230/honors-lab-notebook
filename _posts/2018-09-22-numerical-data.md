---
layout: post
title:  "Numerical Data Doesn't Make Sense"
date:   2018-09-22
---

I’ve been trying to wrap my mind around the idea of the different data formats I’m working with. I wrote a draft of an introduction to the final paper that narrowed the scope of the project down to just convolutional neural networks, and then talked about how I’m going to test primitives with CNNs for image, sound, and numerical data.

This won’t work.

I’m still learning about how machine learning works. I’ve been working out the different types of neural networks. I learned today that convolutional neural networks work best with _spatial_ data: data where the location of the visualized data points matter in relation to each other. Numerical data like shopping trends doesn’t fit this model: you can move the columns and the rows and the meaning doesn’t change.

My introduction doesn’t make much sense. I can’t test CNNs with images, sound, and spreadsheets, since spreadsheet data can’t be fed into a CNN. I’ll have to go back to the drawing board and rethink what I want to test.

The way I see it, there are two possible roads the project can go down. First, I could focus on CNNs, building out a robust sense of primitive generation for spatial data. I could also think about how primitives would work in the context of other neural network types. These would be two very different papers, with two very different experimental setups.

To make this decision, I first want to think about the tech involved. Initial research is bringing me to [Darknet](https://pjreddie.com/darknet/install/), a neural network framework. This looks highly configurable, can take advantage of the GPUs I have at my disposal, and uses C, a language with which I’m very familiar. Darknet seems to require lots of configuration to change network types, so having one CNN I could feed different data into would be helpful (and might also reduce the number of independent variables I have to account for).

Furthermore, the whole concept of primitives doesn’t work for non-spatial data. Primitives, in my mind, end up looking like small matrices that can get combined on a canvas to form one large matrix. This model doesn’t translate well to spreadsheet data, and I’ve been having trouble over the past month imagining how primitives could combine to create that type of data. Intuitively, primitives fit the type of data that would work best using a CNN.

This leads me to believe that the best option for my paper is one in which I still limit myself to CNNs, but also

1. Explain why the primitive model is best used to create spatially significant data, and how that relates to CNNs
2. Find different types of data models (pictures, sound, etc.) that can work with CNNs