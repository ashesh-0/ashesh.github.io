---
layout: single
title: Extreme Precipitation Prediction
permalink: /extreme_rainfall/
author_profile: true
# toc: true
classes: wide
# header:
#     overlay_image: /assets/images/own_collage.jpg
#     overlay_filter: 0.5
#     # image_description: My learnings at Qplum- 3 years zipped into a 10 min read
#     caption: "Photo credit: [**arXiv**](https://arxiv.org/abs/2009.06924)"

---
<!-- https://drive.google.com/file/d/162Cm-Osj_I4qkzgr  qCBYewRX39J8_4YK/view?usp=sharing -->
## Overview
In this project, the aim is to use radar's data to predict the rainfall. In terms of reflectivity, radar waves behave differently depending upon the moisture present in air. As can be seen in the video below, one can see a very clear correlation between radar data and rainfall data.
{% include video id="162Cm-Osj_I4qkzgrqCBYewRX39J8_4YK" provider="google-drive" %}

A simpler problem would be to estimate the rainfall given the radar data. However, our problem is instead to predict the rainfall several hours in advance with a special focus on extreme rainfall.

## Important factors
1. Latitude/Longitude
2. Height above the mean sea level
3. Temporal aspect
4. Seasonality
