---
layout: single
permalink: /SM/DDPM/
author_profile: true
title: "Denoising Diffusion Probabilistic Models"
classes: wide
header:
    overlay_image: /assets/images/score_matching/ddpm.png
    overlay_filter: 0.5
    caption: "Photo credit: [**arXiv**](https://arxiv.org/abs/2006.11239)"

---

## Super Short Description
* [Paper Link](https://arxiv.org/abs/2006.11239)
* This work deals with score matching. Aim is to generate realistic images (from noise). Two markov chains are used. One is parameter-less which sequentially adds noise to the signal (image). The other is its inverse and it converts a noise
to an image sequentially. Deep neural networks are used in the second markov chain. Their novelty is their ability to generate high quality samples from diffusion models. Theoretically, they also show equivalence with denoising score matching with multiple noise levels.

## Concise Overview

### Definitions
* Diffusion process: A Markov chain that gradually adds noise to the data until signal is destroyed.
* Diffusion probablistic model: It is a parameterized markov chain trained which produces samples matching the data after sufficient time. Transitions of this chain uses neural networks. It is also called a reverse process since its aim is to reverse a diffusion process. So, this will start with noise and end with a sample belonging to a data distribution.

Here, the reverse (learnable) process is defined as:
<img src="/assets/images/score_matching/ddpm_reverse.png" alt="drawing"
title="Reverse process"/>

The forward process, a diffusion process with fixed parameters is defined as:
<img src="/assets/images/score_matching/ddpm_forward.png" alt="drawing"
title="Forward process"/>

$$x_0$$ is the clean image. forward process moves from $$x_{0}$$ to $$x_T$$, one step at a time and reverse process moves backwards ($$x_T$$ to $$x_0$$).
### Reverse process
They model the transition probablity using a gaussian distribution
$$p_\theta(x_{t-1}|x_t) = N(x_{t-1};\mu_\theta(x_t,t),\sum_{\theta}(x_t,t))$$. They fix the covariance matrix to a linear multiple of the Identity matrix. As for the mean term, details are shown in the next section.

### Loss
They maximize the log-likelihood of data. They optimize a variational lowerbound of the log-likelihood.
<img src="/assets/images/score_matching/ddpm_loss1.png" alt="drawing"
title="Loss formulation"/>
On simplification, this boils down to 3 KL Divergence terms
<img src="/assets/images/score_matching/ddpm_loss2.png" alt="drawing"
title="Loss formulation in KL Divergence terms"/>

We can use Bayes formula to compute $$q(x_{t-1}\|x_t)$$. It turns out that it is also a gaussian distribution. They denote its mean as $$\widetilde{\mu}_t$$. Since all terms in KL-divergence are comparison between gaussians, this helps them to compute the divergence more efficient when compared with computing using monte carlo estimates. Additionally, since the parameters of forward process are fixed, $$L_T$$ is fixed and therefore can be ignored in training.

$$L_{t-1}$$ can be simplified to:
<img src="/assets/images/score_matching/ddpm_lt_1.png" alt="drawing"
title="The second KL-Divergence term in loss"/>


So, simplest choice is that we make our model predict $$\widetilde{\mu}_t$$. However, after further simplifing $$L_{t-1}$$, another choice arises which essentially directs the model to predict the excess noise present in $$x_t$$ with respect to $$x_{t-1}$$. This happens primarily because $$q(x_t\|x_0)$$ is also gaussian and can be written in a closed form.

### Generating process.
To sample $$x_{t-1}$$ (from $$p_\theta(x_{t-1}\|x_t)$$), one predicts the excess noise $$\epsilon_\theta(x_t,t)$$ and
<img src="/assets/images/score_matching/ddpm_sampling.png" alt="drawing"
title="Image generation by sampling: one step"/>

So, starting from complete noise, one takes backward steps using above formula. At the end, we would have an image belonging to the data distribution.
