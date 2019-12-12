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
