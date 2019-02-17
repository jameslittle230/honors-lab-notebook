---
layout: post
title:  "Model Training Computation Times"
date:   2019-02-14
---

First NBL test
- `nbl-tf-test.config`
- `NUM_TRAIN_STEPS`: 50000
- 29:41:25 CPU time with the K20 GPU
- 17:42:09 CPU time with the RTX 2080 Ti GPU (59.62% of the K20 duration)

Real SVHN Data (*Effectively no difference between the two*)
- 10,000 training data points
  - CPU time: 10:27:53
  - Accuracy at 25k training steps: 6.921
- 60,000 training data points
  - CPU time: 10:43:32
  - Accuracy at 25k training steps: 6.819