---
layout: single
permalink: /diffusion/sm_dae/
author_profile: true
title: "A Connection Between Score Matching and Denoising Autoencoders"
---

## Super Short Description
* [Paper Link](http://www.iro.umontreal.ca/~vincentp/Publications/smdae_techreport.pdf)
* This note looks at multiple score matching objectives. First it explains few score matching objectives which were proved to be equivalent earlier. Next it considers noise related score matching objectives and show a relation between denoising and score matching. For a specific energy function, they show that the denoising autoencoder loss also can be represented as score matching objective.

## Concise Overview
In this paper, there are six formulations of the objective function, all related to score matching. In subsections below, they are briefly described. Let us start with defining some notations:
* The true probablity distribution of x by $$q(x)$$.
* In the hope of mimicking $$q(x)$$, we create a parametrized model $$p(x;\theta)$$ with $$\theta$$ being the learnable parameter.
* Score for a probablity distribution M(x) is defined as $$\psi(x) = \nabla_{x} \log(M(x))$$. We denote the score function of our parametrized distribution $$p(x;\theta)$$ by $$\psi(x;\theta)$$ . Note that the partition function would disappear in the score. This is helpful as in many cases, it is untractable.

### Explicit Score matching
It needs availablity of score of true distribution, $$\nabla_{x} \log(q(x))$$. When that is available, the neural network is trained to output $$\psi(x;\theta)$$.
<img src="/assets/images/score_matching/esm_q.png" alt="drawing"
title="ESM"/>

### Implicit score matching
In most cases, $$\nabla_{x} \log(q(x))$$ is not available. What is available are the iid samples from q. Due to an amazing proof by Hyvärinen (2005), another  objective function was discovered which was  equivalent to Explicit score matching and which did not need $$\nabla_{x} \log(q(x))$$.
<img src="/assets/images/score_matching/ism_q.png" alt="drawing"
title="ISM"/>

Here, d is the dimension of $$x$$. As can be seen from the above expression, trace of the hessian is needed (it is hessian since it is derivative of score, which is in itself a derivative). In order to actually implement it, one needed to replace expectation with sampling.
<img src="/assets/images/score_matching/ism_q0.png" alt="drawing"
title="ISM discrete"/>

### Matching the Score of a Nonparametric Estimator.
In case $$\nabla_{x} \log(q(x))$$ is not available, one way to get that is to use an approximate q by a non-parametric estimation using the iid samples of q. Parzen windows density estimator was used for that. Now that we have an approximate q, one could get target distribution's score function.
<img src="/assets/images/score_matching/esm_qsigma.png" alt="drawing"
title="ESM Estimate"/>
Even with this case, they go ahead to show that similar to explicit score matching,  there exist an equivalent implicit version of it, $$J_{ISMq\sigma}$$, which uses trace of the hessian instead of target distribution's score.

### Denoising Score Matching
Here, they begin with a slightly different problem. Here, the data is the set of pair of clean image and its noisy
version $$ (x,\widetilde{x})$$. They want to estimate conditional probablity density of noisy image given the clean image. Motivation is to be able to denoise the input image. They define the joint probablity density as $$q_\sigma (x,\widetilde{x}) = q_\sigma(\widetilde{x}|x)q(x)$$. Note that $$q(x)$$ is the same as what was used in previous sub sections. The objective is defined as follows:
<img src="/assets/images/score_matching/dsm_qsigma.png" alt="drawing"
title="Denoising score matching"/>

When model is trained, one can get the conditional probablity density using model's output. It is plausible to assume that $$q_{\sigma}(\widetilde{x}|x)$$ will have maximum value when $$\widetilde{x}$$ is equal to $$x$$ (clean image) and will be less when $$\widetilde{x}$$ is noisy. So, when one has score function for $$q_\sigma(\widetilde{x}|x)$$, then one can move $$\widetilde{x}$$ along the score (which is the derivative) to reduce the noise.  They proved that $$DSM_{q\sigma}$$ is equivalent to $$ESM_{q\sigma}$$.
>> So, even if one tries to optimize to denoise the image, the optimal function obtained will be the score function for clean images (when q() is modelled as parzen windows density estimator).

Another work has built on this inference. Instead of training for the score function of clean images, they train on noisy versions of it. At the end, they showed that for specific energy function, the objective function for denoising autoencoder boils down to score matching.
