---
layout: post
title:  "Files and Organization"
date:   2019-02-27
---

## Filename Formats
- `r-*.sh`: Run files; files to submit to the grid
- `m-*/`: Model directories
- `c-*.config`: Config files
- `t-*.tfrecord`: TFRecord files

## Test Name Formats
- `r-10k`: 10,000 data points of real training data
- `r-60k`: 60,000 data points of real training data
- `s-10k`: 10,000 data points of synthetic training data
- `s2-10k`: 10,000 data points of synthetic (Type 2) training data
- `bl50-r-s2-10k`: 10,000 data points of blended training data: 50% real, 50% synthetic II
- `bl10-s1-s2-60k`: 60,000 data points of blended training data: 10% synthetic I, 90% synthetic II
- ... et cetera.h

The test name formats go in the asterisk part of the filename formats above.