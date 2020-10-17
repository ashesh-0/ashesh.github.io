---
layout: single
permalink: /Noise2Void/
author_profile: true
title: "Noise2Void - Learning Denoising from Single Noisy Images"
classes: wide
header:
    overlay_image: /assets/images/noise_to_void_bkg.png
    overlay_filter: 0.5
    # image_description: My learnings at Qplum- 3 years zipped into a 10 min read
    caption: "Source: [**arXiv**](https://arxiv.org/abs/1811.10980)"

---
## Super Short Description
* [Paper Link](https://arxiv.org/abs/1811.10980)
* This paper denoises an image. Novelty of the paper is its ability to train the network without denoised data. Model is trained with a set of images in which some of the images may be clear and some may be noisy. It achieves it by learning to predict a pixel from its neighbouring pixels. In expectation, what the network predicts will be devoid of unstructured noise and therefore it does such a nice job at denoising.

## Brief Description of Main Ideas
### How Blind-Spot Network Works
This is essentially a way to train a denoising network. Given an image, few pixels are randomly selected which the paper addresses as blind spots. For each such pixel, an image patch with the blind spot pixel at its center works as input for the network. In this patch, value of the blind spot pixel is removed from the patch. The original value of the blind spot pixel works as the target. Since, no network can predict the noise, what gets predicted quite close to the denoised pixel value.

### How Blind-Spot Network is Implemented
As discussed above, the network has to take as input an image patch whose central pixel has incorrect value. The network then has to predict the value of that pixel. In implementation, network predicts an image patch of the same size as that of input. While computing the loss, only the central pixel is taken into account. Since the network is fully convolutional, it is not difficult to see and appreciate the fact that in one forward pass, the entire image will get predicted.

### Underlying Assumptions
* *The noise is pixelwise independent:* Value of noise in a pixel should be independent to the value of noise in nearby pixels. In case this assumption doesn't hold, for example in case of presence of intensity gradient in image, that component of noise will remain in the denoised version.
<figure class="half">
    <a href="/assets/images/noise_to_void_orig2.png"><img src="/assets/images/noise_to_void_orig2.png"></a>
    <a href="/assets/images/noise_to_void_den2.png"><img src="/assets/images/noise_to_void_den2.png"></a>
    <figcaption> Original Image (a) has structural noise (tiled effect) along with white noise. Denoised version (c) removes white noise but retains the structural noise (tiled effect) (Credits: https://arxiv.org/abs/1811.10980).</figcaption>
</figure>

* *Data does not have independent pixels:* In case image has very high contrast with pixel values changing almost unpredictably. In that case, the high contract will be blurred as it will be considered as noise.
<figure class="half">
    <a href="/assets/images/noise_to_void_orig.png"><img src="/assets/images/noise_to_void_orig.png"></a>
    <a href="/assets/images/noise_to_void_den.png"><img src="/assets/images/noise_to_void_den.png"></a>
    <figcaption> Original Image (d) has high contrast and pixel values are naturally jittery. Denoised version (f) loses those details (Credits: https://arxiv.org/abs/1811.10980).</figcaption>
</figure>
