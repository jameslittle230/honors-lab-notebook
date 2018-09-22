---
layout: post
title:  "Primitives and the Big Idea"
date:   2018-09-15
---

# Synthetic Training Data

In traditional scenarios, model training can take place only after a lengthy data collection step and an arduous data labeling step; these processes ensure that the resulting data set is suitable for training. In recent history, researchers have been exploring the use of large, computer-generated data sets to train ML models. Instead of collecting and labeling real-world data, a computer algorithm generates a data set that mimics the data that might have been collected naturally. Since the computer algorithm generates each piece of data, it also has insight into specific features of the data, and can thereby label each piece of the data with the learned property as it is generated. With synthetic training data, the onus of the supervisor is no longer to collect and label data; the computer will take care of both of those. Instead, the supervisor must ensure the training data generation algorithm outputs data with a wide enough variety to match the variety seen in testing, while also ensuring that the data remains realistic.

For a synthetic training data set to be successful, it must have the same properties as a high-quality human-curated data set: namely quantity, variety, and similarity. The difficulty in creating such a model synthetically thereby falls to the programmer: they must encode the variety and unpredictability of the real world into an algorithm.

# Primitives

Synthetic training data is not a new idea. Several published applications of ML use synthetic data to either augment or replace the human-supervised data. But the method through which the synthetic data is generated can vary. Many studies use a statistics-based approach: finding the mean and standard deviation of numerical data and generating other data based on these values. Other studies, especially those performing experiments on image data, use 3D modeling to generate a scene and use special rendering techniques to make the render as realistic as possible.

I posit a new method for synthetic data generation, using real-world primitives and using composition techniques to stitch these primitives together. Primitives are real-world samples of individual elements of an entire scene that can be individually manipulated and then combined with other primitives to build a scene. In image data, primitives might be cutouts of different objects in the scene. In sound data, primitives might be individual recordings of footsteps, trees rustling, and background noise. Computers can combine the primitives to create a realistic final scene while still knowing information about the individual primitives.