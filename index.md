---
layout: home
author_profile: true
title: About Me
# layout: single
classes: wide
---
Currently, I'm working as a 3rd year PhD student in [Florian Jug](https://humantechnopole.it/en/people/florian-jug/)'s lab. The broad theme of the lab is to solve biologicaly problems using deep learning. My PhD project is an image decomposition task of splitting a superimposed image into its constituent channels. We recently published our work in [uSplit](https://ashesh-0.github.io/uSplit/) at ICCV 23. Subsequently, we built on top of it to create [denoiSplit](https://arxiv.org/abs/2403.11854), a network which could do unsupervised denoising together with decomposition. This enabled (a) getting multiple predictions (a.k.a opinions of the network) for a single input and (b) model calibration: having a pixelwise estimate of error in the prediction. In my PhD, I also worked on [structural noise removal](/structural_noise_removal/) using contrastive learning on the latent space.

On the coding side, I've been interested in contributing to microscopy data related code: (a) [c-mda-engine](https://github.com/pymmcore-plus/c-mda-engine), a proof-of-concept C++ based engine for controlling microscopes. Idea was to move re-usable code from different downstream applications to a common codebase and use [SWIG](https://www.swig.org/Doc1.3/Python.html) to generate python bindings. (b) I recently (May 2024) started contributing to [microsim](https://github.com/ashesh-0/microsim), a light microscopy simulator.

Prior to this, I was working as a Research Assistant in [National Taiwan University](https://www.ntu.edu.tw/english/), Taipei under Prof. [Hsuan-Tien Lin](https://www.csie.ntu.edu.tw/~htlin/). There, I published two first-author works:
* 3D Gaze estimation in the wild. [BMVC 2021](https://www.bmvc2021-virtualconference.com/conference/papers/paper_0643.html).
* Extreme precipitation prediction. [Problem Statement](/extreme_rainfall/), [Paper Link](https://journals.ametsoc.org/view/journals/aies/1/3/AIES-D-21-0005.1.xml).

I received B.Tech+M.Tech in [Computer Science](https://www.cse.iitd.ernet.in/) in 2015, from the IIT Delhi. I worked as a Data Scientist at [Qplum](/qplum/),  an online investment advisory firm, from Dec 2015 to Dec 2018.


## My pre-PhD research summary
1. Vision: 3D Gaze Estimation: (https://www.bmvc2021-virtualconference.com/conference/papers/paper_0643.html). Created a novel architecture which was more robust to variations in magnification levels. Developed a novel method for backward gazes. Achieved state of the art results on Gaze360 and RT-GENE dataset.

2. Vision: Extreme Rainfall prediction: (https://journals.ametsoc.org/view/journals/aies/1/3/AIES-D-21-0005.1.xml). Using 3D radar data, 2D rain data, altitude data and few others, aim was to predict the rainfall amount in next 3 hours.  An image-to-image translation network with discriminator loss was used to solve this problem.

3. ML in Finance (Industry): Used autoencoder to estimate overall market sentiment which was used to create a market neutral strategy. Used regularized linear regression and other techniques for price prediction.

4. ML on Biomedical Data (Master's Thesis):  Subcellular Regulatory Networks Learning (https://ashesh-0.github.io/Masters/). Jointly learnt gene similarity and gene regulatory network using Markov logic networks.  Generated synthetic data and showed the limitations of our work.
