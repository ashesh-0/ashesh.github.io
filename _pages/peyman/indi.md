---
layout: single
permalink: /diffusion/indi/
author_profile: true
classes: wide
title: "Inversion by Direct Iteration: An Alternative to Denoising Diffusion for Image Restoration"
toc: false
header:
    overlay_image: /assets/images/indi_overview.png
    overlay_filter: 0.5
    caption: "Photo credit: [**arXiv**](https://arxiv.org/abs/2303.11435)"

---
## Super Short Description
* [Paper Link](https://arxiv.org/abs/2303.11435)
*  This paper focuses on the problem of image restoration: one has access to clean and degraded image pairs but not the degradation operator. Similar to diffusion models, the authors propose a iterative method of taking multiple small restoration steps to eventually restore the degraded image. In this way, they avoid "regression to the mean" effect. This work outperforms several other contemporary works on perceptual metrics. Due to the existance of perceptual-distortion tradeoff and the fact that their approach explicitly aims for perceptual prowness, it does not outperform on distortion metrics (which is perfectly understandable).

## Training 
The authors work with a dataset of clean and degraded image pairs, $$(x,y)$$. For training, they create an intermediate image, $$x_t$$ by taking a linear combination of the clean and degraded image. They train a network, $$F_{\theta}$$ to predict clean image $$x$$ where the inputs are the intermediate image $$x_t$$ and the mixing coefficient, denoted here by $$t$$. The training objective is shown below: 
 ![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/indi_objective.png){: .align-center}

## Inference
At inference time, $$F_{\theta}(x_t,t)$$ gives an estimate of the clean image. The idea is to get a better estimate of $$x$$, denoted here by $$\hat{x}_{t - \delta}$$, by taking a weighted average of current prediction and existing estimate as shown below. Additionally, for faster convergence, they add a small amount of gaussian noise  to $$\hat{x}_{t-\delta}$$ (not shown in the equation below).  
![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/indi_inference.png){: .align-center}

## Demonstrating InDI effectiveness to "regression to the mean" effect
They create two synthetic small datasets, one of which is shown below. Data comes from a multi-modal dirac delta distribution with 4 points (orange dots). The degradation is gaussian noise and so the degraded observations are all over the place (blue dots). The left panel below shows the clean and degraded data. In the right panel we have InDI's prediction (black empty circles) and a single step MMSE estimate (red filled circles). While InDi is able to recover the original points (black circle perfectly encircles organge dots), the single step restoration leads to predictions which are essentially weighted averages of the four points (red dots).       
![image-center]({{ site.url }}{{ site.baseurl }}/assets/images/indi_synthetic.png){: .align-center}
## Its relation to other generative models
It is related to diffusion models and flow matching in the sense that both InDI and diffusion model take multiple small steps for image restoration. However, InDI does not require the degradation operator and hence is more practical than vanilla diffusion models. InDI is also closely related to flow matching. InDI requires some amount of gaussian noise to be present in the degraded images but that is not an explicit requirement in flow matching. The authors also show that InDI is closely related to residual flow. Specifically, they show that as $\delta$ goes to 0, the iterative inference procedure of InDI converges to an ordinary differential equation (ODE) which can be interpreted as residual flow.