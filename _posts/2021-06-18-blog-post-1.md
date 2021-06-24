---
title: 'Implicit neural representations'
date: 2021-06-24
permalink: /notes/implicit-neural-representations/
tags:
  - representations
---

A MLP takes as input pixel coordinates and is trained to output the intensity value of that pixel. The training is done for a single image (using different pixels as training datapoints). After training, we may evaluate the MLP at a denser grid of coordinates to give a super-resolved image. Alternatively, the MLP can be stored as a compressed version of the image (the complexity of the MLP grows with the complexity of the image content, but not with the image size). Thus. the MLP is an implicit representation of the image (v/s the explicit pixel coordinate-intensity value representation). Also, the MLP is a continuous representation as it can be evaluated at continuous valued inputs, while the pixel representation is a discrete one.

A MLP with Relu / sigmoid activations is not able to learn such a mapping well, even on the training data. MLPs with sinusoid activations can do this though ([SIREN](https://arxiv.org/pdf/2006.09661.pdf)). Another way to get this to work is to first pass the coordinates through a 'fourier feature mapping' and then through the MLP ([Random Fourier Features](https://arxiv.org/pdf/2006.10739.pdf)).

