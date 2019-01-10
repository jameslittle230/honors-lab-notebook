---
layout: post
title:  "Midterm Presentation: Exploring the Viability of IBSG For Training ML Detectors"
date:   2018-12-10
---

*This is adapted from presentation that I gave at the end of the first semester, explaining the exploratory work I've done so far on the project.*

With this project, I've been looking at Isolation Based Scene Generation (IBSG), a methodology for generating synthetic training data for neural networks. IBSG, I argue, is used best to solve detection-based problems, especially those where humans can intuitively perform the detection (but might not have enough bandwidth to do so).

## Machine Learning Background

Machine learning is complicated, but one way of understanding it is in its name. A machine learns how to solve a specific, well-defined problem, instead of relying on a person to solve the problem and encode the solution in an algorithm. 

When humans write algorithms, they might follow this series of steps:

1. **Understand the problem.** To write an algorithm that sorts numbers in a list, one must have a good understanding of what a number is, how they can exist sequentially, and what a list of numbers is.
2. **Figure out a way to transform input into output.** Algorithm designers should nail down the desired input, desired output, and design a methodology to transform the first into the second.
3. **Describe that transformation using logical steps.** This might look like a flowchart that precisely describes how to transform that input. For every run of the flowchart, the output should 
4. **Encode those logical steps using code.** Code is a textual representation of the flowchart from above, with one difference: a computer can read through it and transform it into executable instructions. Code is an intermediary between the human form of the solution and the computational form.

When computers write an algorithm, they’re not trying to write code that nicely describes the problem, since code is mostly written for human consumption (the computer eventually just compiles it into CPU instructions anyway). Instead, the machine is trying to come up with a mathematical function that will transform a specific type of input into the output that a researcher desires.

![](/img/function.png)

Since humans aren’t involved in the learning process, the function can be pretty mysterious. It’s not always possible to look at the design of the function, and when it is, it’s nearly impossible to understand why it works the way it does: in many cases, this function will look like a series of intense linear equations with no apparent meaning. This seems less than useful at first, until you consider that we turn to machine learning when humans wouldn't be able to figure out how to write a similar algorithm. To use the example above, we wouldn't use machine learning to generate a function that sorts lists, since humans can write that algorithm very easily. Instead, though, we would train a machine to detect soccer balls in images like this one:

![](/img/boxed-ball.png)

Figuring out where to draw the box isn’t an easy problem; Bowdoin students have spent a long time (with limited success) trying to build an algorithm to do so. If we can build a program that will teach a computer how to build that algorithm for us, we can spend our time working on other things.

### Artificial Neural Networks

Artificial Neural Networks are one of the leading ways of implementing machine learning. They are based on the neural mechanisms that take place in the brain, in which neurons transmit information via synapses: spaces between axons and dendrites crossed by small amounts of electrical potential.

![](/img/ffann.png)

Feed-forward artificial neural networks, shown above, can be thought of as directed graphs. Series of interconnected nodes are organized into layers, and each node in a layer is connected to every node in the layer before and the layer after that one. There are three types of layers in a feed-forward artificial neural network:

- The **Input Layer** nodes store the individual piece of input: for image data, each pixel value is stored in a different node.
- The **Hidden Layer** nodes store intermediary transformations. They don't mean anything on their own, but could be thought of as steps in the computer's algorithmic flowchart.
- The **Output Layer** nodes store the results: the probability that something is true, for example.

Every node has an activation function: a function that turns all the node's inputs into a single value. Every node also has a bias, a threshold that that function's output should be in order for the node to propagate information. Every edge (connection between two nodes) has a weight: a connection strength between those two nodes.

Weights and biases (generally floating point values between 0 and 1) are the values that the computer teaches itself; the activation functions and layer specifications are set by the researcher ahead of time.

### Training

Weights and biases are set through a training process, in which a computer adjusts those values until the hidden layers accurately transform input into expected output. The training process requires a *labeled training data set*: a dataset of archetypal inputs and the desired output that the function should get. The training process takes a form such as this one:

1. Set all the weights and biases to random numbers.
2. Send all the inputs from the training data through the function and compare the *calculated* outputs with the *expected* outputs.
3. Tweak the weights and biases in different directions
4. Find a direction that minimizes the error—the difference between calculated and expected outputs
5. Repeat those steps until the error gets to be below a desired threshold

Once the machine converges on a function with a low enough error value, one can be confident that the probability of error when the function sees an unknown input will be similarly low.

The quality of a labeled training data set can make or break the success of a neural network. I have identified four properties that a good labeled training data set will have:

![](/img/training-data.png)

1. **Accuracy:** the outputs for a given input should be well-formed.
2. **Quantity:** MNIST, the "Hello World" of ML training data sets, has 60,000 training data points.
3. **Variety:** Data points should not all look the same. For example, MNIST includes data points written by dozens of different people. The example above is what it looks like when I write numbers all in the same way.
4. **Realism:** Data points should match the test data as closely as possible. A sample of the handwriting fonts on my computer won’t match people’s actual handwriting.

## Computers and Training Data

Generally, humans are used to label training data. This often results in very high quality training data sets: accuracy is good depending on what you're trying to label, and variety and realism are both easy because you can give your labelers a subset of your collected data (and the variety and realism will come for free). Quantity, though, is expensive. It takes two work weeks for a single person to label 60,000 soccer ball images like the one above. In some cases, this isn't feasable: academics and workers often do not have two spare work weeks available to exclusively label data.

An alternative to human-labeled data is computer-synthesized (and therefore, computer-labeled) data. If a computer can generate training data, it can label it automatically. This stacks up fairly well with our four properties of good training data: accuracy is guaranteed, variety isn’t difficult because the data can be generated randomly, quantity is incredibly cheap. The challenge becomes one of realism: how can data generated by a computer match closely enough real-world data? Synthetic data generation processes are only recently being researched; my project looks at one method—IBSG—and tests whether it can be a drop-in replacement for real, hand-labeled training data.

### IBSG

Isolation Based Scene Generation involves making generalizations about the scenes in a dataset and figuring out which isolations (or ingredients) make up those scenes.

<div style="width: 50%; float: right; margin-left: 20px;">
<img src="/img/isolations.jpg">
</div>

This image might be split up into three different isolations: soccer balls, robots, and soccer fields. The researcher would identify these isolations and extract them, building different examples of extracted isolations that can be mixed and matched.

Those isolations (and the final scene as a whole) can also take on modifications: changes that further randomize the resulting scene and that increase that scene's realism. As an example, I noticed that the robotic soccer images would often have motion blur, so I introduced a global motion blur modification with a random magnitude that would get applied to the scene.

The researcher then builds a program that blends those isolations into a reconstructed scene, randomly placing the isolations and incorporating both the isolation-level and the global modifications. The data can be labeled at the time of synthesis, since the computer knows the properties of the isolations it is randomly placing.

Data I've generated with IBSG (examples below) is not perfect—it clearly looks computer generated. But in some scenarios, this might not matter. Throughout the following semester, I'm testing whether the not-quite-there realism afforded with IBSG is enough to train a neural network to accurately classify data when it sees new, real-world inputs.

![](/img/ibsg.jpg)

## IBSG In Use

IBSG is not a catch-all tool: it is not an ideal choice for all machine learning scenarios, since the process is based on human perception. Humans compose a scene by identifying component parts and understanding how they work together. IBSG requires that humans identify objects that can be individually detected, so that those humans can describe isolations that build up a scene. When we see an image, we use our own ability to decompose it to choose what the isolations and modifications will be to regenerate a scene. In this way, IBSG is best used for visual and auditory data, especially when those datasets are rich, complex blends of multiple distinct sources.

IBSG is helpful when meaningful data (for example, a soccer ball) is obscured, and when we can label a scene with information readily available to the computer. Scenes that humans can't percieve easily like financial data or other large numeric datasets are not candidates for IBSG: it is incredibly difficult to find the isolations and modifications present in a spreadsheet.

Because of the input limitations (what humans can percieve and separate) and the output limitations (what computers know when they're generating a scene), it can be concluded that IBSG works best for creating audio or visual scenes where we’re trying to output the presence, absence, or location of one of the isolations. In the context of machine learning problems, this is known as object detection. The problems IBSG can help answer are: is an element a part of a scene? And if so, where is it?

## My Experiment

In my experiment, I hope to answer three big questions:

- Should I use IBSG-trained neural nets?
- How do I make a really good IBSG dataset?
- Once I have an IBSG dataset, how should I use it?

Throughout the project, I plan on building several IBSG datasets based on freely available, real-world datasets. I'll train many different neural networks with different IBSG and real training data configurations, and compare the testing accuracy of all those neural networks. In doing so, I'll figure out what works when building an IBSG dataset and what doesn't.

I plan on basing my IBSG datasets on four existing datasets:

- [Street View House Numbers](http://ufldl.stanford.edu/housenumbers/)
- [Common Objects in Context](http://cocodataset.org/#home)
- [Warblr](http://machine-listening.eecs.qmul.ac.uk/bird-audio-detection-challenge/)
- [OpenSLR](http://www.openslr.org/12/)

The first two are visual, made up of photographic images that can be easily decomposed. The second two are auditory, made up of real-world recordings with individual, detectable parts.

The experiment controls for several variables, most importantly the neural network hyperparameters. I'm not testing different neural network configurations; in fact, I've outsourced the design of the network itself to TensorFlow researchers by using their [Object Detection](https://github.com/tensorflow/models/tree/master/research/object_detection) framework. Instead, I want to modify three variables:

- Composition of IBSG dataset (real vs. synthetic)
- Number of isolations
- Amount of modifications

and with different configurations of these variables, observe the effect on the percentage of real data correctly identified. Progress will be presented on this blog as I go.

*Thanks to Prof. Eric Chown for advising and Prof. Steve Majercik for reading. For questions, feel free to get in touch.*