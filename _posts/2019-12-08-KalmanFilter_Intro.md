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

# Prediction Models for Process and Measurement of a System
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

Since all the information provided by $$\mathbb{Z}_{k-1}$$ is already incorporated in $$x_k$$, without loss of generality, we can say that $$p(z_k \vert \mathbb{Z}_{k-1}, x_k) = p(z_k \vert x_k)$$. Then the above equation is further simplified to,

$$p(x_k \vert \mathbb{Z}_k) = \frac{p(z_k \vert x_k)p(x_k \vert \mathbb{Z}_{k-1})}{p(z_k \vert \mathbb{Z}_{k-1})}$$

Therefore,

$$p(x_k \vert \mathbb{Z}_k) \propto p(z_k \vert x_k)p(x_k \vert \mathbb{Z}_{k-1})$$

$$p_{posterior_k} \propto p_{measurement_k} * p_{prior_k}$$

We can make two key observations from the last equation, at any time step k.
1. Knowing the pdf of the measurement and prior, the posterior distribution can be computed.
2. The prior $$p(x_k \vert \mathbb{Z}_{k-1}) = \int_{R_{x_{k-1}}}p(x_k \vert x_{k-1})p(x_{k-1} \vert \mathbb{z}_{k-1})$$. So there is a recursive relationship.

Note that, despite having an insightful analytical expression to find posterior of the states at a time step $$k$$, they can not be implemented as a computer program, the integrals can not be expressed in closed form expression. That sets the topic of the next section.

# Posterior Estimation Problem as Mean, Covariance Estimation Problem
Knowing the fact that mean of a normally distribution random variable is same as the expected value of the random variable, in this section we will pose the posterior estimation problem as mean, covariance estimation problem. Before we proceed, let me define some notations first.
- $$\hat{x}_k^+ = \mathbb{E}[x_k \vert \mathbb{Z}_k] \rightarrow$$ Mean of the posterior estimate
- $$\hat{x}_k^- = \mathbb{E}[x_k \vert \mathbb{Z}_{k-1}] \rightarrow$$ Mean of the prior estimate
- $$\tilde{x}_k^- = x_k - \hat{x}_k^- \rightarrow$$ Prediction error
- $$\hat{z}_k = \mathbb{E}[z_k \vert \mathbb{Z}_{k-1}] \rightarrow$$ Mean of the measurement
- $$\tilde{z}_k = z_k - \hat{z}_k \rightarrow$$ Measurement innovation

The subscript $$k$$ is the time index. Please note that,

- In practice we can not compute $$\tilde{x}_k^-$$, since, true value, $$x_k$$ is unknown.
- It can be shown that $$\tilde{x}_k^-$$ and $$\tilde{z}_k$$ are both zero mean Gaussians, with covariance matrices same as that of $$x$$ and $$z$$ respectively. Thus, $$\Sigma_{\tilde{x}} = \Sigma_{x}$$ and $$\Sigma_{\tilde{z}} = \Sigma_{z}$$.

Notice that,

$$\mathbb{E}[\tilde{x}_k^- \vert \mathbb{Z}_k]  = \mathbb{E}[x_k - \hat{x}_k^- \vert \mathbb{Z}_k]$$

$$\mathbb{E}[\tilde{x}_k^- \vert \mathbb{Z}_k]  = \mathbb{E}[x_k \vert \mathbb{Z}_k] - \mathbb{E}[\hat{x}_k^- \vert \mathbb{Z}_k]$$

Using the definitions of $$\hat{x}_k^+$$ and $$\hat{x}_k^-$$ we get,

$$\mathbb{E}[\tilde{x}_k^- \vert \mathbb{Z}_k]  = \hat{x}_k^+ - \hat{x}_k^-$$

$$\hat{x}_k^+ = \hat{x}_k^- + \mathbb{E}[\tilde{x}_k^- \vert \mathbb{Z}_k]$$

Since $$\tilde{x}_k^-$$ already incorporates all the measurement information up to $$\mathbb{Z}_{k-1}$$, we can say that, $$\mathbb{E}[\tilde{x}_k^- \vert \mathbb{Z}_k] = \mathbb{E}[\tilde{x}_k^- \vert z_k]$$. Then we can simplify the above euation as,

$$\hat{x}_k^+ = \hat{x}_k^- + \mathbb{E}[\tilde{x}_k^- \vert z_k]$$

Using the process prediction model, we can compute the $$\hat{x}_k^-$$, but we do not know yet how to compute $$\mathbb{E}[\tilde{x}_k^- \vert z_k]$$. In order to derive the expression of $$\mathbb{E}[\tilde{x}_k^- \vert z_k]$$ in a more tractable form, we will be using the identity with out proof that, for two random variables $$X$$ and $$Z$$

$$\mathbb{E}[X \vert Z] = \mathbb{E}[X] + \Sigma_{XZ}\Sigma_Z^{-1}(Z - \mathbb{E}[Z])$$.
