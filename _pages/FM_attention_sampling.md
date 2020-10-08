---
layout: single
title: Modality Attention and Sampling Enables Deep Learning with Heterogeneous Marker Combinations in Fluorescence Microscopy

permalink: /MAS_FM/
author_profile: true
# toc: true
classes: wide
header:
    overlay_image: /assets/images/MAS_FM_3.png
    overlay_filter: 0.5
    caption: "Photo credit: [**ArXiv**](https://arxiv.org/abs/2008.12380)"

---
## Super Short Introduction
* [Paper Link](https://arxiv.org/abs/2008.12380)
* Target here is to do image segmentation. This paper works with Fluorescence Microscopy (FM) data. One data point in FM dataset comprises of a set of images, each corresponding to a specific marker and has a distinct distribution. Not all data points have same number of markers. Aim is to do the segmentation using images belonging to whichever markers are present. This is done using a single network for better generalization. Novelty of the paper is in its sampling based approach while training allowing it to handle arbitrary subset of markers and in its attention based technique allowing it to explicitly feed in the information about which markers are present.

## Brief Description of the Main Ideas

### Marker Sampling (MS)
With marker sampling, one randomly selects a subset of markers which will be processed by the segmentation network. This makes the network capable to handle any subset of markers at test time.

### Marker Excite (ME)
It is an attention based mechanism for reweighting the features learnt at intermediate layers. Input to the attention module is one hot encoded marker presence data. As with a typical attention module, Marker Excite allows the network to adjust better to the presence of any random subset of markers. They use the UNet network for segmentation. They replace the pre-existing attention module with Marker Excite attention at multiple intermediate layers as shown below.
<figure>
    <a href="/assets/images/MAS_FM_2.png"><img src="/assets/images/MAS_FM_2.png"></a>
    <figcaption>Showing Marker Excite Attention (Orange arrow) in UNet architecture (Credits: https://arxiv.org/abs/2008.12380).</figcaption>
</figure>

### Network Architecture
Network architecture is shown in the below figure. From the multi-marker data, one acquires multiple 2D images, one for each marker. Marker Sampling is performed and selected images are passed through the network to get segmentation. Note that since the input of the network is of fixed dimension, a 2D array of zeros is passed for those markers which are either absent in the data or have been deselected by Marker Sampling.
<figure>
    <a href="/assets/images/MAS_FM_1.png"><img src="/assets/images/MAS_FM_1.png"></a>
    <figcaption>Network Architecture(Credits: https://arxiv.org/abs/2008.12380).</figcaption>
</figure>
