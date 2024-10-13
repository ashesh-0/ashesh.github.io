---
layout: home
author_profile: true
title: About Me
# layout: single
classes: wide
---
Currently, I'm working as a 3rd year PhD student in [Florian Jug](https://humantechnopole.it/en/people/florian-jug/)'s lab. 
My PhD project is an image decomposition task of splitting a superimposed image into its constituent channels. 

I received B.Tech+M.Tech in [Computer Science](https://www.cse.iitd.ernet.in/) in 2015, from the IIT Delhi. 
I worked as a Data Scientist at [Qplum](https://attck.com/work/qplum/),  an online investment advisory firm, from Dec 2015 to Dec 2018.
I then worked as a Research Assistant in [National Taiwan University](https://www.ntu.edu.tw/english/), Taipei under Prof. [Hsuan-Tien Lin](https://www.csie.ntu.edu.tw/~htlin/) where I worked in Computer Vision.

# PhD
Given a superimposed (noisy) image, the task is to decompose it into its constituent channels.
<img src="assets/images/usplit_teaser.png" alt="drawing" class="center" width="800px" height="auto"
title="Splitting: An image decomposition task"/>

We published [uSplit](https://ashesh-0.github.io/uSplit/), a HVAE inspired architecture which used surrounding context in a GPU-efficient way, at ICCV 23. Subsequently, we built on top of it to create [denoiSplit](https://arxiv.org/abs/2403.11854), a network which could do unsupervised denoising together with decomposition.
This enabled (a) getting multiple predictions (a.k.a opinions of the network) for a single input and (b) model calibration: having a pixelwise estimate of error in the prediction. 
We recently published it at ECCV 24.
For a meaningful evaluation of our work, and in general for unsupervised denoising tasks on microscopy data, we developed [microSSIM](https://ashesh-0.github.io/MicroSSIM/), a variant of SSIM more suited for microscopy data which was published at BIC workshop, ECCV 24. 
At the beginning of my PhD, I also worked on [structural noise removal](/structural_noise_removal/) using contrastive learning on the latent space.


## Code Contributions
On the coding side, I've been interested in contributing to microscopy data related code: (a) [c-mda-engine](https://github.com/pymmcore-plus/c-mda-engine), a proof-of-concept C++ based engine for controlling microscopes. Idea was to move re-usable code from different downstream applications to a common codebase and use [SWIG](https://www.swig.org/Doc1.3/Python.html) to generate python bindings. (b) I recently (May 2024) started contributing to [microsim](https://github.com/ashesh-0/microsim), a light microscopy simulator. (c) I created a python package [predtiler](https://pypi.org/project/predtiler/), a light-weight package which enables tiled prediction in any dataset class used with pytorch with minimal changes in the dataset class code.

# RA in Vision-lab, NTU, Taiwan.
Prior to this, I was working as a Research Assistant in [National Taiwan University](https://www.ntu.edu.tw/english/), Taipei under Prof. [Hsuan-Tien Lin](https://www.csie.ntu.edu.tw/~htlin/). There, I published two first-author works:
* 3D Gaze estimation in the wild. [BMVC 2021](https://www.bmvc2021-virtualconference.com/conference/papers/paper_0643.html).
* Extreme precipitation prediction. [Problem Statement](/extreme_rainfall/), [Paper Link](https://journals.ametsoc.org/view/journals/aies/1/3/AIES-D-21-0005.1.xml).

