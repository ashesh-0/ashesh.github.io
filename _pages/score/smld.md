---
layout: single
permalink: /SM/SMLD/
author_profile: true
# classes: wide
title: "Generative Modeling by Estimating Gradients of the Data Distribution"
toc: true
header:
    overlay_image: /assets/images/score_matching/SMLD.jpg
    overlay_filter: 0.5
    caption: "Photo credit: [**arXiv**](https://arxiv.org/abs/1907.05600)"

---
## Super Short Description
* [Paper Link](https://arxiv.org/abs/1907.05600)
*  This work is based on score matching. The primary concern tackled by the paper is that natural images lie in a small manifold and large part of the space does not contain any real examples. They tackle the difficulties arising from above fact by adding gaussian noise of different magnitudes to the image so as to cover whole space.

## Brief Overview of the Methodology
### Definitions
* Score for a probablity distribution M(x) is defined as $$\psi(x) = \nabla_{x} \log(M(x))$$.

### Main Issue Which They Tackle
Real images lie in a high dimensional space (A 512*512 image lies in $$\rm I\!R^{262144}$$). Naturally, most of the
space does not contain relevant images. In such regions, the score $$\psi(x)$$ is not defined. Secondly, in regions of low density, the score estimation will be less accurate.

### Noise Conditional Score Networks (NCSN)

#### Noisy Samples
They work with gaussian distribution to inject noise. They start with standard deviation for these gaussian distributions
$$\{\sigma_i\}_{i=1}^L$$. They define the perturbed data distribution as $$q_\sigma(x) \overset{\Delta}{=}\int p_{data}(t) N(x\|t,\sigma^2I)dt$$

With contraint that $$\sigma_i = \lambda*\sigma_{i+1}, \forall i\in[1,L]$$ with $$\lambda >1$$, they have a progressively less noisy distribution ($$q_{\sigma 1}(x)$$ is most noisy and $$q_{\sigma L}(x)$$ is least noisy).

For generating a noisy sample from q_{\sigma k}, one starts with a clean image and adds a gaussian noise to it from $$N(0,\sigma_k^2)$$

#### On learning
For each $$\sigma_k$$, they work with following denoising score matching objective $$l(\theta;\sigma)$$:
<img src="/assets/images/score_matching/SMLD_obj.png" alt="drawing"
title="Objective"/>
Note that since the conditional probablity here is modelled as a gaussian, its score can be analytically computed to $$\dfrac{\widetilde{x} - x }{\sigma^2}$$. They use a unified objective over all $$\sigma$$s
<img src="/assets/images/score_matching/SMLD_obj2.png" alt="drawing"
title="Unified objective"/>


#### NCSN inference via annealed Langevin dynamics
They start with a random noise image and iteratively convert it to a realistic image. For doing this, they follow the same procedure for every $$\sigma_i$$. At every noise level, they update the image in the direction of the score for T steps. When updating the image, they also add a noise component to it at every step. They then take this as the initial input for the next noise level and do the same procedure.
<img src="/assets/images/score_matching/SMLD_sample.png" alt="drawing"
title="Iterative generation"/>


### Why it works
It has been proven in previous works that Denoising score matching objective makes the model predict score for $$q_\sigma(x)$$ and not for $$q_\sigma(\widetilde{x}\|x)$$. So, if $$\sigma$$ is very small, then the model learns to predict score of $$q(x)$$, the real data distribution. In this work, they keep the $$\sigma_L$$ to be super small so that above logic works. Also, they keep $$\sigma_1$$ to be super large so that it spans the whole space and one can easily sample from it.
