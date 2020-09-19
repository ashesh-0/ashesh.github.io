---
layout: single
permalink: /learning_by_synthesis/
author_profile: true
title: "Learning-by-Synthesis for Appearance-based 3D Gaze Estimation"

# header:
#     image: /assets/images/dual_resol_corres_net.png
#     # overlay_filter: 0.5
#     # image_description: My learnings at Qplum- 3 years zipped into a 10 min read
#     caption: "Source: [**arXiv**](https://arxiv.org/abs/2006.08844)"

---

## Super short introduction
* [Paper Link](https://ieeexplore.ieee.org/document/6909631)
* Here, they introduce a new dataset for 3D Gaze estimation. Another novelty of the paper is data generation procedure. Using 8 cameras, they are able to reconstruct 3D structure of eye-region using which they generate augmented data by varying the virtual camera and projecting the 3D points onto the virtual camera screen. This yields eye-region with novel head poses. They use regression forest for estimating the gaze.

## Brief overview
### Dataset Description
The dataset has 64K images which comprises of 50 subjects, 8 views (head poses) and 160 gaze directions.
<figure class="half">
    <a href="/assets/images/lbs_2013_1.png"><img src="/assets/images/lbs_2013_1.png"></a>
    <a href="/assets/images/lbs_2013_2.png"><img src="/assets/images/lbs_2013_2.png"></a>
    <figcaption>Left:Placement of virtual camera at fixed distance from eye. Right: Definition of head pose. Head pose is defined by the 3D coordinate of mid point of eyes and the face plane (plane of the triangle) (Credits: https://ieeexplore.ieee.org/document/6909631).</figcaption>
</figure>

### Generation of Synthetic Data
Head pose is defined by the 3D coordinate of eye midpoint and the normal vector of the face plane in the camera coordinate system. They make the original observation that a virtual camera can be introduced such that camera-person distance is fixed to some value. With this configuration, using the two angles in the polar coordinates, the camera position can be determined.
They then go on to change the virtual camera position by changing the projection matrix of the camera. They compute the required transformation which needs to be applied to gaze, head pose and the eye image so that all of them are in the new virtual camera coordinate system. This assumes eye region to be planar.

### Head Pose based Data Division
They note that head pose determines the range in which the gaze can vary. The actual gaze can be estimated by looking at iris contours. They therefore divide the dataset into overlapping head pose bins and create one model (random regression forest) for each bin.
### Model Setup
They use Decision trees to estimate the head pose. As mentioned in previous section, they divide the dataset into overlapping head pose bins and create one model (random regression forest) for each bin.  Within each bin, they build Q binary regression trees which trains on a random subset of the data of that bin.
