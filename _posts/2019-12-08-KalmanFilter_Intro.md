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

# Bayes Rule to Find Posterior
Let $$\mathbb{Z}_k$$ denotes the set of measurement sequences $${z_0, z_1, z_2, \dots, z_k}$$. Then according to Baye's rule,

$$p(x_k \vert \mathbb{Z}_k) = \frac{p(\mathbb{Z}_k \vert x_k) p(x_k)}{p(\mathbb{Z}_k)}$$

$$p(x_k \vert \mathbb{Z}_k) = \frac{p(z_k,\mathbb{Z}_{k-1} \vert x_k) p(x_k)}{p(z_k, \mathbb{Z}_{k-1})}$$

Using the rule of joint pdf that $$p(a, b) = p(a \vert b) p(b)$$, we can rewrite the above equation as,

$$p(x_k \vert \mathbb{Z}_k) = \frac{p(z_k \vert \mathbb{Z}_{k-1}, x_k) p(\mathbb{Z}_{k-1} \vert x_k) p(x_k)}{p(z_k \vert \mathbb{Z}_{k-1}) p(\mathbb{Z}_{k-1})}$$

Further using the joint pdf rule to the term $$p(\mathbb{Z}_{k-1} \vert x_k)$$ we write,

$$p(x_k \vert \mathbb{Z}_k) = \frac{p(z_k \vert \mathbb{Z}_{k-1}, x_k) p(x_k)}{p(z_k \vert \mathbb{Z}_{k-1}) p(\mathbb{Z}_{k-1})} \frac{p(x_k \vert \mathbb{Z}_{k-1})p(\mathbb{Z}_{k-1})}{p(x_k)}$$

Simplifying we get,

$$p(x_k \vert \mathbb{Z}_k) = \frac{p(z_k \vert \mathbb{Z}_{k-1}, x_k)p(x_k \vert \mathbb{Z}_{k-1})}{p(z_k \vert \mathbb{Z}_{k-1})}$$
<!-- p(z_k \vert \mathbb{Z}_{k-1}, x_k) = p(z_k \vert \mathbb{Z}_{k-1}, x_k)-->

Since all the information provided by $$\mathbb{Z}_{k-1}$$ is already incorporated in $$x_k$$, without loss of generality, we can say that $$p(z_k \vert \mathbb{Z}_{k-1}, x_k) = p(z_k \vert x_k)$$. Then the above equation is further simplified to,

$$p(x_k \vert \mathbb{Z}_k) = \frac{p(z_k \vert x_k)p(x_k \vert \mathbb{Z}_{k-1})}{p(z_k \vert \mathbb{Z}_{k-1})}$$

Therefore,

$$p(x_k \vert \mathbb{Z}_k) \propto p(z_k \vert x_k)p(x_k \vert \mathbb{Z}_{k-1})$$

$$p_{posterior_k} \propto p_{measurement_k} * p_{prior_k}$$

We can make two key observations from the last equation, at any time step k.
1. Knowing the pdf of the measurement and prior, the posterior distribution can be computed.
2. The prior $$p(x_k \vert \mathbb{Z}_{k-1}) = \int_{R_{x_{k-1}}}p(x_k \vert x_{k-1})p(x_{k-1} \vert \mathcal{Z}_{k-1})$$. So there is a recursive relationship.

  <!--image: "/images/posts/kalman_post_header_image.png"-->
