---
layout: post
title:  "Thoughts on Data Formats"
date:   2018-09-07
categories: post
---

Convolutional neural nets just take in a set of numbers and output a set of numbers. The exact numbers that go in (and the exact numbers that come out) depend on what the actual inputs are and what the intended output is. For example, a perceptron that detects whether an object is present in an image might take in pixel data as inputs and give back a single boolean value (1 or 0) that represents whether the object is present.

The nature of that pixel data is variable; if it’s black and white, one number might represent the grayscale value of each pixel. If it’s a color image, three numbers might represent the red, green, and blue values of each pixel. The model will be based on the image size: pixel number 650 might be at the top left of a 640x480 image, but in the bottom of a 26x26 image. There’s no intrinsic connection between a specific value location (a number at input index 650, for example) and what it represents *beyond* the model it’s part of.

Artificial data generation *can’t* be generalizable because it’s intrinsically tied to the problem domain: we’re not able to come up with augmentation methods that will work for images, audio, and sensor data. We have to creatively find **primitives** that are represented in the data, then alter those primitives to generate artificial data points.

This could be worth exploring. If we generate some data using statistical methods (generating random numerical inputs based on standard deviation and mean, for example) and pit it against data built from altered primitives, I wonder which scenarios would be better for which data set?
