---
title: "Kalman Filter: Introduction and Intuition"
date: 2019-12-08
tags: [Estimation Theory, Filtering Methods, Bayesian Inference]
header:
excerpt: "Kalman Filter for Scientists and Engineers"
---

Kalman filter is an iterative algorithm, to compute sequence of inner hidden states of a process given the sequence of sensor measurement information of the measurable states. Following the Baye's inference rule, the estimated hidden states are the posterior distributions given the prior distribution of those states. The prior distributions of the states are computed using a mathematical process model of the system.

One of the key assumption of Kalman filter, is that, all the *probability distribution functions (pdf)* need to be Gaussian distributions.

In order to implement Kalman filter, we need two mathematical models,
1. Process model (used to predict the prior of the estimation)
2. Measurement model (used to predict the measurement)

Another key assumption in Kalman filter is that, the Process Model and Measurement Model has to be linear in terms of the parameters. Although, extended Kalman Filter do not need this linearity assumption.

# Prediction Models of Dynamic System


  <!--image: "/images/posts/kalman_post_header_image.png"-->
