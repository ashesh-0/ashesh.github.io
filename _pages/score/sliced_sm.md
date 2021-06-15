---
layout: single
permalink: /SM/SSM/
author_profile: true
title: "Sliced Score Matching: A Scalable Approach to Density and Score Estimation"
---

## Super Short Description
* [Paper Link](https://arxiv.org/abs/1905.07088)
* This work deals with score matching. Aim is to speed up the training process for score matching. They come up with a new method for it and show theoretically that it is equivalent to original method. They show that their new method is faster. In their method, instead of taking fisher divergence between target score and the predicted score, they project the scores onto some random direction and then take the difference.

## Concise Overview

### Definitions
* $$p_d$$: Data distribution
* $$\widetilde{p}_m(x;\theta)$$: Unnormalized density (modelled by a neural network)
* $${p}_m(x;\theta)$$: Corresponding normalized density
* Score function: Score for a probablity distribution M(x) is defined as $$\nabla_{x} \log(M(x))$$.
* $$s_d$$ and $$s_m$$ denote the score functions for $$p_d()$$ and $$p_m()$$ respectively.
* Score matching: One has a data distribution, typically in implicit form with i.i.d samples drawn from it. Objective is to train a network which predicts score of that distribution.
### Earlier Work
In work done by Hyvärinen (2005), for score matching fisher divergence was established to be the objective of choice. The objective $$L(\theta)$$ is defined as
<img src="/assets/images/score_matching/ssm_fisher2005.png" alt="drawing"
title="Score matching objective"/>

In that work it was shown that there exist an equivalent objective which does not need the score of the target distribution, $$s_d(x)$$. It is a beautiful proof using integration by parts.
<img src="/assets/images/score_matching/ssm_fisher2005_2.png" alt="drawing"
title="Implicit score matching objective"/>

Here, $$tr$$ is the trace. Notice that $$p_d()$$ is just in the expectation which can easily be approximated by monte carlo estimate. So here, one needs to compute the trace of the hessian. This brings us to the central issue tackled by the paper.

### Issue
If $$D$$ is the dimension of data, then our model outputs score which has $$D$$ scalar values. We need to compute the partial derivative of output's each dimention for computing the trace. So, this will take $$D$$ times more time over computing partial derivative of a scalar.

### Sliced Score Matching
Instead of using the fisher divergence, they use the following expression for objective:
<img src="/assets/images/score_matching/ssm_slicedfisher.png" alt="drawing"
title="Sliced score matching objective"/>

Here, v is some random direction. So, this objective first projects the actual score and the predicted score to a random direction and then computes the difference. Note that expectation is also taken with respect to v. On the lines of proof done by Hyvärinen (2005), they prove an equivalent objective which does not need $$s_d$$.


<img src="/assets/images/score_matching/ssm_implicit_slicedfisher.png" alt="drawing"
title="Implicit sliced score matching objective"/>

> Now, the benefit is that $$v^T s_m(x;\theta)v$$ is a scalar. So, one needs D times less time to compute
$$\nabla_{x}v^T s_m(x;\theta)v$$.
