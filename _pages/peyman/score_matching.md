---
layout: single
permalink: /diffusion/score-matching/
author_profile: true
classes: wide
title: "Soft Diffusion Score Matching for General Corruptions"
toc: false
header:
    overlay_image: /assets/images/peyman_score_matching_scheduler.jpg
    overlay_filter: 0.5
    caption: "Photo credit: [**arXiv**](https://arxiv.org/abs/2209.05442)"

---
## Super Short Description
* [Paper Link](https://arxiv.org/abs/2209.05442)
*  This paper aims to establish a principled way of training a diffusion model for removing arbitrary linear corruptions which can be modelled by a matrix multiplication with the input. There are overall three contributions: 1. Soft score matching: a novel training objective. They show its relationship with the DSM (Denoising score matching) objective. 2. Momemtum sampler: More detailed image generation along with increased diversity is achieved. 3. Scheduling: They quantify shift in distribution on adding degradation and thereby provide a principled way of deciding how much overall degradation should be at each step.     

## Soft score matching

The authors work with linear corruptions which could be modelled by a matrix multiplication as denoted by $$C_t$$ below (blur). 
![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/peyman_score_matching_degradation.png){: .align-center}

The extend the DSM equivalence proof (Vincent 2011) to the case of such corruptions, i.e, in the equations shown below, minimizing $$J_1(\theta)$$ is same as minimizing $$J_2(\theta)$$. Specifically, under "mild" conditions, one only needs conditional log-likelihood to learn the score.
<figure>
    <a href="/assets/images/peyman_score_matching_dsm.png"><img src="/assets/images/peyman_score_matching_dsm.png"></a>
    <figcaption> Degradation family considered in this paper (Credits: https://arxiv.org/abs/2209.05442).</figcaption>
</figure>
 

### Uncleared Doubt

 The do a network reparametrization making use of the given linear corruption matrix. 
 Instead of moving the network prediction $$s_{\theta}(x|t)$$ closer to $$(C_t* x_0 - x_t)/\sigma^2_t$$, 
 they instead predict $$h_{\theta}$$, which is related to $$s_{\theta}$$ as shown below.
 ![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/peyman_score_matching_reparametrization.png){: .align-center}
 <!-- <figure>
    <a href="/assets/images/peyman_score_matching_reparametrization.png"><img src="/assets/images/peyman_score_matching_reparametrization.png"></a>
    <!-- <figcaption> Degradation family considered in this paper (Credits: https://arxiv.org/abs/2209.05442).</figcaption> -->
<!-- </figure> -->

Hence, now, $$C_t*h_{\theta}(x|t)$$ 
now is trained to be close to $$C_t * x_0$$. While it is clear that it is a reparametrization and that the knowledge about the degradation is used, it is not clear what is the advantage of this reparametrization. An ablation study on this would have been helpful.
 
## Momentum Sampler

 They look at their formulation as a Stochastic differential equation (SDE) and they argue that their SDE formulation is reversible. They discretize the reverse diffusion process to obtain an expression for $$\Delta x$$, which when added to $$x_t$$, moves it closer to $$x_0$$. The expression for $$\Delta x$$ is shown below.
 <figure>
    <a href="/assets/images/peyman_score_matching_scheduler_expression.png"><img src="/assets/images/peyman_score_matching_scheduler_expression.png"></a>
    <!-- <figcaption> Degradation family considered in this paper (Credits: https://arxiv.org/abs/2209.05442).</figcaption> -->
</figure>
It is worth noting that there are three expressions above. The first one is doing deblurring (Notice the difference is being taken between the degradation matrices) and the second one is doing denoising. One could also see below the qualitative effect of the momentum sampler.
 
 
 <figure>
    <a href="/assets/images/peyman_score_matching_scheduler.jpg"><img src="/assets/images/peyman_score_matching_scheduler.jpg"></a>
    <figcaption>(Credits: https://arxiv.org/abs/2209.05442).</figcaption>
</figure>

 
## Scheduling
 
 The authors note that if one degradation step is too large, the network may not be able to learn the score. The quantify the step size by the distance between the two adjacent distributions. They pick the number of intermediate degradation distributions such that the distance between the two adjacent distributions is upper bounded by a given threshold. This threshold denotes the maximum shift in distribution that the network can handle. 
