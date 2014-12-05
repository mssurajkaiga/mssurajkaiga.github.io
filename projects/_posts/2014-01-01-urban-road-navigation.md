---
date: 2014-01-01
layout: projects_post
title: Monocular Vision Based Road Detection and Following
---

Single Camera based Road Following has been done mainly using Vanishing point estimation. This method assumped that the road region is triangular in shape and road boudaries are visible. For challenging situations like extremely curved shaped roads, the method does not give good results. In order to improve upon this we implemented the following pipeline:

* Shadow removal using entropy minimization assuming plankian illumination.

* Road Segmentation using region growing and non-parametric model

* Set of reference point extraction and using those as alternatives to vanishining points for navigation.

* Smooth Navigation using PID for a differential drive robot.
 
The road segmentation work was a re-implementation of the work of **Jose M Alvarez** in his IVS 2008 paper on [*Illuminant-Invariant Model-Based Road Segmentation*](http://www.cvc.uab.es/~jalvarez/IlluminantInvariantModelBasedRoadSegmentation.pdf).
Our entire pipeline was published at the proceedings of the International Conference on Machine Vision and Machine Learning. You can find the paper [here](http://avestia.com/MVML2014_Proceedings/papers/127.pdf).
