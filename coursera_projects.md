---
layout: single
author_profile: true
title: Projects from Coursera
toc: true
---

Coursera courses, if done **honestly** and **thoroghly** equips one with all the necessary concepts and practical tips for doing a project in that field. After doing 10 courses related to deep learning, I can vouch for this fact.

Let me take you through one course [Deep Learning in Computer Vision!](https://www.coursera.org/learn/deep-learning-in-computer-vision). Since I intend to take not more than 15 minutes of your time, I'll take the liberty of giving you an aerial view of the course and zooming in only on few places.

## Pre deep learning era
They pick up the topic from eye anatomy and enter the vision field by discussing elemental things like brightness, contrast, causes of poor contrast, frequency etc. I had taken both computer graphics course and computer vision course in my college and yet these few minutes videos taught me so many new things. I certainly don't claim that these weren't taught in my college. May be I wasn't receptive enough for full 40 minutes ;). Anyways, let me spend some time on **Image Contrast**.
> Poor contrast happens when there is not sufficient variation in brightness among nearby pixels. One simple instance is when not full range of brightness is used in the image. After knowing this, scaling up the brightness by a linear transformation then becomes a natural fix for the problem.
\$$x' = 255* (x - x_{min})/(x_{max} - x_{min})$$

Linear transformation formula written above will make sure that $$x'$$ varies in $$[0,255]$$. But then what if image has regions of very high and very low brightness and still has poor contrast? Well, then the linear transformation will not work since $$x_{max} - x_{min} \approx255$$. Then they introduce Gamma transformation where one improves the contrast in dark regions at the cost of reduction of contrast in bright regions. \$$x' = c*x^\gamma, \gamma < 1$$

Contrast increases in dark regions as we decrease gamma. By taking $$\gamma=0.5, c=10$$ , let me convince you of this. Points with brightness value of 225 and 196 will now have 150 and 140 brightness respectively. Brightness difference between these points decreased. However, points with brightness of 1 and 4 will now have brightness of 10 and 20 respectively. Brightness difference has increased !

Then they go on to introduce kernels, kernels for gradient estimation, Canny edge detection etc.

## CNN based applications
In the second week, they switch gears and go on to cover Image categorization, Fine grained recognition, Content based Retrieval and Face keypoint regression all in one week !
### Parameter efficient Filter decomposition
They certainly start with basic concepts like convolution, filters. They go on to explain the parameter efficient decomposition of filters:
> A $$5*5$$ filter can be approximated by two $$3*3$$ filters. Assuming N to be the number of input and output channels, $$25*N^2$$ is the parameter count for $$5*5$$ filter. $$2*9*N^2$$ is the parameter count for two $$3*3$$ filters, thereby achieving 28% reduction in parameter count.

One can further decompose $$3*3$$ into $$3*1$$ and $$1*3$$. They go on to explain the dimensionality reduction property of $$1*1$$ convolution. Then they go on to explain building blocks of Inception network, Residual network, Stochastic depth policy and so on.

### Fine grained image recognition
In Fine grained image recognition, they take time to explain the peculiarity of the problem. One instance of the problem would to to classify between different variety of birds. One should not that for the same bird type we will have significantly different images depending on bird pose and surrounding environment. Further, there will be images belonging to different bird types but will have relatively similar images owing to sameness in environment and/or pose.
> Fine grained image recognition problem has high intra class variance (due to difference in orientation and surrounding) but low inter-class variance (due to similarity among different classes).

### Face: Attributes, Recognition, Keypoints
For detection of facial attributes (gender, age, etc) they explained the global and the local approach. Global way is to extract features from the entire face. In this version, face landmarks are not needed. This method is however not robust to orientation changes. Local way is to detect object parts, extract features from each part and then predict the attributes by using all features.

Face recognition comes in two forms: Verification and Identification. Given two images, **Face verification** tries to find whether they belong to same person. One can use a pre-trained backbone to get embeddings for both images, compute the eucledean distance between the embeddings and using the optimal threshold, one can then classify whether both images belong to same person. They introduce **Triplet loss** for training. This loss takes 3 images, two of which belong to the same person. Let *f* be the embedding function. Let $$I_a,I_p$$ and $$I_n$$ are the input images where $$I_a$$ and $$I_p$$ belong to same person. This loss ensures that:
\$$ || f(I_a) - f(I_p)|| + \alpha < || f(I_a) - f(I_n)|| $$

> In words, Triplet loss tries to make sure that distance between embeddings of two images of the same person is $$ \alpha$$ less than distance between images of different persons. This helps to find a stable threshold for the Face Verification problem.

Given an image, **Face identification** solves a much harder version of correctly matching it with one entry of the face database. Things get even more harder in the Open set version of the problem where we don't know whether there is some entry which actually matches with the given face image.
They go on to discuss Keypoints regression problem. Later they describe CNN Cascade: a hierarchy of neural networks as a way to stablize the prediction.


