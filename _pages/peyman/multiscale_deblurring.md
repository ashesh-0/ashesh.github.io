---
layout: single
permalink: /multiscale-deblurring/
author_profile: true
# classes: wide
title: "Multiscale Structure Guided Diffusion for Image Deblurring"
toc: true
header:
    overlay_image: /assets/images/peyman_deblurring_intro.jpg
    overlay_filter: 0.5
    caption: "Photo credit: [**arXiv**](https://arxiv.org/abs/2212.01789)"

---
## Super Short Description
* [Paper Link](https://arxiv.org/abs/2212.01789)
*  This paper tackles deblurring task and works with Conditional diffusion model based setup where the conditional input is the blurry image. The primary focus is on out-of-distribution performance. The technical novelty lies in how the conditional input is mixed with the intermediate noisy $$x_t$$.  

## Learned Structural Guidance

### Motivation
In order to improve the out-of-distribution performance, the authors ensure two things. Firstly, more and more coarser scale information is encouraged to be used. This should help since it is more likely that even in test images, which are out-of-distribution, the coarse scale information is still similar to what was seen in training data. Secondly, the relevant information present in the conditional input has an 'optimal' representation before merging with $$x_t$$.

### Implementation details
The conditional input, which is a blurry image, is downsampled multiple times. For each downsampled version, a guidance network is trained in a supervised way to predict the clean image version of the blurry image at the corresponding resolution. This ensures that the network learns to extract the most relevant information from the blurry image. 
<figure>
    <a href="../assets/images/peyman_deblurring_multiscale_setup.png"><img src="../assets/images/peyman_deblurring_multiscale_setup.png"></a>
    <figcaption> Learned Structural guidance (Credits: https://arxiv.org/abs/2212.01789).</figcaption>
</figure>

The latent representation of each of these downsampled versions are then merged with the corresponding latent representation of the UNet, the restoration module of the diffusion model.
<figure>
    <a href="../assets/images/peyman_deblurring_overall.png"><img src="../assets/images/peyman_deblurring_overall.png"></a>
    <figcaption> Overall model architecture (Credits: https://arxiv.org/abs/2212.01789).</figcaption>
</figure>
