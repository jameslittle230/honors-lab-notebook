---
layout: post
title:  "About This Lab Notebook"
date:   2018-07-21 09:49:35 -0700
categories: post
---
## Why this site?

During my final year at Bowdoin, I’ll be working on an [Honors Project](https://www.bowdoin.edu/academic-handbook/academics/honors.shtml): a year-long independent research project that acts as the culmination of my academic studies. I’m doing my project under the Computer Science department, advised by Professor [Eric Chown](http://bowdoin.edu/~echown).

> The honors project can be the culmination of a student’s academic experience at Bowdoin and offers an unparalleled chance for intellectual and personal development.

Pretty cool.

I’m writing this the summer before my senior year, when the project is being fleshed out but work on it has not begun (clearly, since this is the first entry in the lab notebook). The project brief is, informally, to build a neural-network-based ball detection system for [RoboCup robots](https://www.youtube.com/watch?v=r7XT98HchBs). More specifically, this means:

1. Training a machine-learning model to accurately detect the position and size of RoboCup SPL soccer balls within a frame of video
2. Building or adapting a perceptron that will run locally on the robot and detect these balls in real-time
3. Determine whether this perceptron is better or worse than the existing ball-detection solution

As this is an academic project, I need some way of recording progress and keeping track of resources. Most projects in the sciences have lab notebooks associated with them. This is a project in the *computer* sciences, so it has a *computer* lab notebook. Pretty fancy!

## Why this project?

Ball detection is a huge part of RoboCup success, and since the SPL changed the ball from a bright orange one to a black-and-white one, it has been one of our weak points. No other team in the SPL is using a completely machine-learned solution, and I believe that it can be done.

Part of the challenge will be building a neural net to run on the robot: the computing power in the [Aldebaran Naos](https://en.wikipedia.org/wiki/Nao_(robot)) is weak, and traditional machine-learning frameworks will take too many computing resources. Instead, I will be building a perceptron that is both low-scope and low-power: it only needs to detect balls, but it needs to do so quickly and simply.

## What to expect?

I’ll be posting journal entries each day I work on the project, long-form posts when I am able to come to longer conclusions, and resources I use (books, articles, videos, etc.) to help me in my learning. This will be the place to keep up with my project, and will be a place where I, when writing the final paper, will reference to figure out what I did all year.

A rough timeline of events is as follows:

* **By October:** Build a set of training data through artificial means
* **By Thanksgiving:** From the training data, build a model
* **By March:** Build a perceptron that uses the model
* **By April:** Run the perceptron on a robot
* **By May:** Final tweaks for accuracy, write a paper, give a presentation

Looks pretty ambitious!