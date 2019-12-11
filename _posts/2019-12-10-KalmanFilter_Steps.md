---
title: "Kalman Filter: An Implementation Perspective"
date: 2019-12-08
tags: [Estimation Theory, Filtering Methods, Bayesian Inference]
header:
excerpt: "Kalman Filter: Basic Steps"
mathjax: "true"
---
This post will summarize the basic steps required to implement Kalman filter in as a computer program. For this particular post, we will not assume the linearity of the process or measurement models, instead we will assume a generic model and derive Kalman Filtering steps for them.

We will divide the prediction and update step each into three sub-steps.

For any time step $$k$$,

**A. Prediction step**

1. Based on the prior measurements $$\mathbb{Z}_{k-1}$$, compute the expected value of the prior prediction $$\hat{x}_k^-$$.

$$\hat{x}_k^- = \mathbb{E}[x_k \vert \mathbb{Z}_{k-1}] = \mathbb{E}[f_{k-1}(x_{k-1}, u_{k-1}, w_{k-1}) \vert \mathbb{Z}_{k-1}]$$

2. Determine the error covariance of the prior state estimate.

$$\Sigma_{\tilde{x}_k}^- = \mathbb{E}[(\tilde{x}_k^-)(\tilde{x}_k^-)^T]$$

3. Predict the measurement using prior state estimate.

$$\hat{z}_k = \mathbb{E}[z_k \vert \mathbb{Z}_{k-1}] = \mathbb{E}[h_k(x_k, u_k, v_k) \vert \mathbb{Z}_{k-1}]$$

**B. Correction/Update step**

1. Compute the Kalman gain matrix.

$$l_k = \Sigma_{\tilde{x}_k\tilde{z}_k}^-\Sigma_{\tilde{z}_k}^{-1}$$

2. Determine expected state vector of the posterior estimation.

$$\hat{x}_k^+ = \hat{x}_k^- + L_k(z_k - \hat{z}_k)$$

3. Compute the covariance matrix of the posterior estimation.

$$\Sigma_{\tilde{x}_k}^+ = \mathbb{E}[(\tilde{x}_k^+)(\tilde{x}_k^+)^T]$$

$$\Sigma_{\tilde{x}_k}^+ = \Sigma_{\tilde{x}_k}^- - L_k\Sigma_{\tilde{z}_k}L_k^T$$
