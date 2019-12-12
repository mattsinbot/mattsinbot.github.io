---
title: "Kalman Filter: Linear System"
date: 2019-12-08
tags: [Estimation Theory, Filtering Methods, Bayesian Inference]
header:
excerpt: "Kalman Filter: Basic Steps"
mathjax: "true"
---

In this post, I will derive each steps that has been presented in [Kalman Filter: An Implementation Perspective]{https://mattsinbot.github.io/KalmanFilter_Steps/} for a system which has linear process and measurement models.

A system is called linear if the *process* and *measurement* models are linear with respect to the parameters. The linear process and measurement models can be defined as,

$$x_k = A_{k-1}x_{k-1} + B_{k-1}u_{k-1} + w_{k-1}$$

$$z_k = C_kx_k + D_ku_k + v_k$$

The process and measurement noise vectors $$w_k$$ and $$z_k$$ are uncorrelated white Gaussians. Further to note that, these noises are zero mean and known covariance matrices.

$$\mathbb{E}[(w_k)(w_k)^T] = \Sigma_{\tilde{w}}$$, $$\mathbb{E}[(v_k)(v_k)^T] = \Sigma_{\tilde{v}}$$ and $$\mathbb{E}[(w_k)(x_0)^T]=0$$.

**Prediction step - 1A:** Expected prior estimate

$$\hat{x}_k^- = \mathbb{E}[f_{k-1}(x_{k-1}, u_{k-1}, w_{k-1}) \vert \mathbb{Z}_{k-1}]$$

$$= \mathbb{E}[A_{k-1}x_{k-1} + B_{k-1}u_{k-1} + w_{k-1} \vert \mathbb{Z}_{k-1}]$$

$$= \mathbb{E}[A_{k-1}x_{k-1} \vert \mathbb{Z}_{k-1}] + \mathbb{E}[B_{k-1}u_{k-1} \vert \mathbb{Z}_{k-1}] + \mathbb{E}[w_{k-1} \vert \mathbb{Z}_{k-1}]$$

$$= A_{k-1}\mathbb{E}[x_{k-1} \vert \mathbb{Z}_{k-1}] + B_{k-1}\mathbb{E}[u_{k-1} \vert \mathbb{Z}_{k-1}] + 0$$

$$= A_{k-1}\hat{x}_{k-1}^+ + B_{k-1}\hat{u}_{k-1}$$

**Prediction step - 2A:** Compute the prediction error

$$\tilde{x}_k^- = x_k - \hat{x}_k^-$$

$$=\left(A_{k-1}x_{k-1} + B_{k-1}u_{k-1} + w_{k-1}\right) - \left(A_{k-1}\hat{x}_{k-1}^+ + B_{k-1}u_{k-1} \right)$$

$$=(A_{k-1}\left(x_{k-1} - \hat{x}_{k-1}^+\right) + w_{k-1}$$

$$\tilde{x}_k^- = A_{k-1}\tilde{x}_k^+ + w_{k-1}$$

Therefore, the covariance of the prediction error is,

$$\Sigma_{\tilde{x}_k}^- = \mathbb{E}[(\tilde{x}^-)(\tilde{x}^-)^T]$$

$$= \mathbb{E}[\left(A_{k-1}\tilde{x}_{k-1}^+ + w_{k-1}\right)\left(A_{k-1}\tilde{x}_{k-1}^+ + w_{k-1}\right)^T]$$

$$= A_{k-1}\mathbb{E}[(\tilde{x}_{k-1}^+)(\tilde{x}_{k-1}^+)^T]A_{k-1}^T + 2\mathbb{E}[w_{k+1}\tilde{x}_{k+1}^{+T}]A_{k-1}^T + \mathbb{E}[(w_{k+1})(w_{k+1})^T]$$

$$\Sigma_{\tilde{x}_k}^- =  A_{k-1}\Sigma_{\tilde{x}_{k-1}^+A_{k-1}^T + \Sigma_{\tilde{w}}$$

**Prediction step - 2C:** Predict measurement

$$\hat{z}_k = \mathbb{E}[h_k(x_k, u_k, v_k) \vert \mathbb{Z}_{k-1}]$$

$$= \mathbb{E}[C_kx_k + D_ku_k + v_k \vert \mathbb{Z}_{k-1}]$$

$$= \mathbb{E}[C_kx_k \vert \mathbb{Z}_{k-1}] + \mathbb{E}[D_ku_k \vert \mathbb{Z}_{k-1}] + \mathbb{E}[v_k \vert \mathbb{Z}_{k-1}]$$

$$\hat{z}_{k} = C_k\hat{x}_k^- + D_ku_k$$
