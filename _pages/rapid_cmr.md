---
layout: single
title: Rapid whole-heart CMR with single volume super-resolution
permalink: /rapidCMR/
author_profile: true
header:
    overlay_image: /assets/images/rapidCMR_2.png
    overlay_filter: 0.5
    caption: "Photo credit: [**JCMR**](https://jcmr-online.biomedcentral.com/articles/10.1186/s12968-020-00651-x)"

---
## Super Short Introduction
* [Paper Link](https://jcmr-online.biomedcentral.com/articles/10.1186/s12968-020-00651-x)
*  This paper uses a residual U-Net architecture for super-resolution of whole heart CMR images. Low resolution acquisition followed by fast super-resolution results in 3X speed up over direct high resolution acquisition.

## Work Overview
### Synthetic Training Data
For supervised training to get high-resolution data from low-resolution input, one needs paired low and high resolution data. High resolution data (WH-bSSFP) was obtained from medical sources. It was converted to K-space. Outer 50% of the data in both directions was zeroed out. This was followed by 'asymmetric zeroing in K-space'. This was then converted back to CMR image space resulting in low resolution data. Note that for testing the generalizability, varying amount of data points in the K-space are zeroed out.

### Broad Inferences
In general, vessel diameters were correctly depicted in super-resolution images. However, one could observe slight underestimation of vessel diameter for the case of proximal left coronary artery(LCA). In terms of lesion detectivity and specificity, high resolution data was better than super-resolution data which was in turn better than low resolution data. However, the difference between high resolution and super-resolution were marginal. In terms of image quality, super-resolution data was the best with sharp,clear edges and denoised images (it had the best eSNR).
<figure>
    <a href="/assets/images/rapidCMR_1.png"><img src="/assets/images/rapidCMR_1.png"></a>
    <figcaption>One can observe good reconstruction in the case of super-resolution. (Credits: https://jcmr-online.biomedcentral.com/articles/10.1186/s12968-020-00651-x)</figcaption>
</figure>

### Limitations
The primary limitation is that the data excluded rarer defects and just considered mainstream issues. So one natural extension of the work can be to intelligently encorporate more conditions. Another limitation is related to image normalization. For some cases (not present in training/test data), images may have very high valued pixels. In such cases, normalization can certainly lead to lower valued pixels which could then effect the performance adversely.Another limititation is regarding the richness of training data. Firstly, MR data is complex valued. Here, magnitude was used and the phase component was ignored. Secondly, MR data is retrieved from multiple coils. Here, a pre-processed form of it was used where multiple-coil data was combined. For a better quality reconstruction, one can look into working with raw data.

