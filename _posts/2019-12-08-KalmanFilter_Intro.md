---
title: "Kalman Filter: Introduction and Intuition"
date: 2019-12-08
tags: [Estimation Theory, Filtering Methods, Bayesian Inference]
header:
excerpt: "Kalman Filter for Scientists and Engineers"
mathjax: "true"
---

Kalman filter is an iterative algorithm, to compute sequence of inner hidden states of a process given the sequence of sensor measurement information of the measurable states. Following the Baye's inference rule, the estimated hidden states are the posterior distributions given the prior distribution of those states. The prior distributions of the states are computed using a mathematical process model of the system. In particular we are interested in computing the posterior *probability distribution functions (pdf)* $$p(x_k \vert z_k)$$.

One of the key assumption of Kalman filter, is that, all the *pdf* need to be Gaussian distributions.

In order to implement Kalman filter, we need two mathematical models,
1. Process model (used to predict the prior of the estimation)
2. Measurement model (used to predict the measurement)

Another key assumption in Kalman filter is that, the Process Model and Measurement Model has to be linear in terms of the parameters. Although, extended Kalman Filter do not need this linearity assumption.

# Prediction Models of Dynamic System
The process and measurement models can be written generally in discrete form as,

$$x_k = f_{k-1}(x_{k-1}, u_{k-1}, w_{k-1})$$

$$z_k = h_k(x_k, u_k, v_k)$$

where, $$u_k \rightarrow$$ known input signal, $$w_k \rightarrow$$ process noise and $$v_k \rightarrow$$ measurement noise. Further, if the process and measurement functions are linear then we can write,

$$x_k = Ax_{k-1} + Bu_{k-1} + w_{k-1}$$

$$z_k = Cx_{k} + Du_{k} + v_{k}$$

In the probabilistic world with Gaussian pdf assumption, the first equation can be used to compute the mean of the pdf $$p(x_k \vert x_{k-1})$$ and the second equation to compute the mean of measurement pdf $$p(z_k \vert x_k)$$. Next we will show how we can use the pdf $$p(x_k \vert x_{k-1})$$ and pdf $$p(z_k \vert x_k)$$ to compute pdf $$p(x_k \vert z_k)$$ using Baye's rule, which we ultimately care about.





  <!--image: "/images/posts/kalman_post_header_image.png"-->
