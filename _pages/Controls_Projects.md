---
title: "Controls Projects"
permalink: /controlsprojects/
header:
  # image: "/images/deeplearning.jpg"
---

### Design of Neuro-Observer of Robots
In this project we synthesized a nonlinear system-state-observer for two single-input-single-output
nonlinear systems. We use neural network to capture nonlinearity of the observer. No linearity
with respect to the unknown system parameters is required for the designed observer. The observer
stability and boundedness of the state estimates and NN weights are proven. In order to show the
effectiveness of the proposed observer, two simulations are carried out. First we modeled NN based
observer for a single-link robot, rotating in vertical plane with two sets of example data sets to train
the NN embeded into the observer. The second observer is designed for Van der Pol oscillator. For
the single-link observer, tests are performed with no-noise training data set and with noisy dataset
as well. It has been observed that NN based observer learned more accurately and faster from the
no-noise data set as compared to noisy data set which leads to longer learning time.
The github link for this project can be found [here](https://github.com/mattsinbot/Neuro-Observer-for-Dynamical-Systems).
