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

$$\mathbb{E}[(w_k)(w_k)^T] = \Sigma_{\tilde{w}}$$ and $$\mathbb{E}[(v_k)(v_k)^T] = \Sigma_{\tilde{v}}$$ and $$\mathbb{E}[(w_k)(x_0)^T]=0$$.

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

**Prediction step - 3C:** Predict measurement

$$\hat{z}_k = \mathbb{E}[h_k(x_k, u_k, v_k) \vert \mathbb{Z}_{k-1}]$$

$$= \mathbb{E}[C_kx_k + D_ku_k + v_k \vert \mathbb{Z}_{k-1}]$$

$$= \mathbb{E}[C_kx_k \vert \mathbb{Z}_{k-1}] + \mathbb{E}[D_ku_k \vert \mathbb{Z}_{k-1}] + \mathbb{E}[v_k \vert \mathbb{Z}_{k-1}]$$

$$\hat{z}_{k} = C_k\hat{x}_k^- + D_ku_k$$

**Update step - 1B:** Determine Kalman gain matrix

We already have derived Kalman gain matrix in the [post](https://mattsinbot.github.io/KalmanFilter_Intro/) as
$$L_k = \Sigma_{\tilde{x}_k\tilde{z}_k}^- \Sigma{\tilde{z}_k}^{-1}$$

Next we will first derive the two covari6ance matrices on the right hand side for a linear system and then combine them.

*Find* $$\Sigma{\tilde{x}_k\tilde{z}_k}^{-}$$

$$\Sigma{\tilde{x}_k\tilde{z}_k}^{-} = \mathbb{E}[\tilde{x}_k^- (C_k\tilde{x}_k^- + v_k)^T]$$

$$= C_k^T\mathbb{E}[\tilde{x}_k^-\tilde{x}_k^{-T}] + \mathbb{E}[\tilde{x}_k^-v_k^T] = C_k\Sigma_{\tilde{x}_k}^-$$

*Find* $$\Sigma{\tilde{z}_k}$$

$$\tilde{z}_k = z_k - \hat{z}_k = \left(C_kx_k + D_ku_k + v_k\right) - \left(C_k\hat{x}_k^- + D_ku_k\right)$$

$$\tilde{z}_k = C_k\tilde{x}_k^- + v_k$$

Therefore,

$$\Sigma_{\tilde{z}_k} = \mathbb{E}[(C_k\tilde{x}_k^- + v_k)(C_k\tilde{x}_k^- + v_k)^T]$$

$$= C_k\mathbb{E}[(\tilde{x}_k^-)(\tilde{x}_k^-)^T]C_k^T + 2\mathbb{E}[v_k\tilde{x}_k^-]C_k^T + \mathbb{E}[(v_k)(v_k)^T]$$

$$= C_k\Sigma_{\tilde{x}_k}^-C_k^T + \Sigma_{\tilde{v}}$$

Combining the results we get,

$$L_k = \left(C_k\Sigma_{\tilde{x}_k}^-\right)\left(C_k\Sigma_{\tilde{x}_k}^-C_k^T + \Sigma_{\tilde{v}}\right)^{-1}$$

**Update step - 2B:** Find the mean of posterior estimation

$$\hat{x}_k^+ = \hat{x}_k^- + L_k(z_k - \hat{z}_k)$$

**Update step - 3B:** Find the covariance of posterior estimation

$$\Sigma_{\tilde{x}_k}^+ = \Sigma_{\tilde{x}_k}^- - L_k\Sigma_{\tilde{z}_k}L_k^T$$

$$= \Sigma_{\tilde{x}_k}^- - L_k\Sigma_{\tilde{z}_k}\left(\Sigma_{\tilde{x}_k\tilde{z}_k}^-\Sigma_{\tilde{z}_k}^{-1}\right)^T$$

Using the fact that covariance matrices are symmetric and simplifying we get,

$$\Sigma_{\tilde{x}_k}^+ = \Sigma_{\tilde{x}_k}^- - L_k\Sigma_{\tilde{x}_k\tilde{z}_k}^-$$

Using the fact that, $$\Sigma{\tilde{x}_k\tilde{z}_k}^{-} = C_k\Sigma_{\tilde{x}_k}^-$$ we get,

$$\Sigma_{\tilde{x}_k}^+ = \Sigma_{\tilde{x}_k}^- - L_kC_k^T\Sigma_{\tilde{x}_k}^-$$

This completes the derivations of the steps of Kalman Filter of a Linear System.
