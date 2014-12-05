---
author: mssurajkaiga
comments: true
date: 2014-03-25 16:25:18+00:00
layout: post
slug: realistic-rendering-basic-1
title: Realistic Rendering - [Basic] - 1
wordpress_id: 28
categories:
- computer graphics
- rendering
tags:
- basic
- computer graphics
- ray tracing
- rendering
---

As my research interest lies in Computer Graphics, primarily rendering, I have been studying upon topics to gain more knowledge on it. I am starting a series of beginner posts that will hopefully be helpful to both me and others who wish to delve into this field. Also, to catch up with my current progress, I might do some posts which might be quite ahead of this series. I also assume that the reader's will be familiar with some basic computer graphics and related geometry. That being said, let's begin.

Rendering is a principal part of Computer Graphics. It's the process which converts a description of a 3-D scene into a 2-D image that can be viewed on a screen. Lot of exciting research is happening in this field including artistic rendering, cloth rendering, cartoon rendering and obviously photo-realistic rendering.

Rendering can be sub-divided into real-time rendering (online rendering) or pre-rendering (offline rendering). Real-time rendering renders the scene in a few milliseconds and allows users to modify/navigate the scene smoothly. On the other hand offline rendering does very large amount of computations consuming a large amount of time but generally creates a much more realistic image. I will be starting with topics on realistic rendering and then proceed onto real-time rendering techniques. Here are some very realistic images that have been created by artists and researchers:

[![real0](http://mssuraj.files.wordpress.com/2014/03/real0.jpg?w=300)](http://mssuraj.files.wordpress.com/2014/03/real0.jpg) [Jarosz et al. 2008]

[![real1](http://mssuraj.files.wordpress.com/2014/03/real1.jpg?w=300)](http://mssuraj.files.wordpress.com/2014/03/real1.jpg) [Jakob et al. 2010]

[![real2](http://mssuraj.files.wordpress.com/2014/03/real21.jpg?w=300)](http://mssuraj.files.wordpress.com/2014/03/real21.jpg)[Jorge Jimenez et al. 2011]

How exactly is a scene represented? What were the stuff involved in the process of "rendering" such images? These are some of the questions that arise when you see these pictures. Note that all the three pictures were generated as part of very advanced research and development. As technology develops, its becoming difficult to distinguish from real worlds and virtual worlds. My intention is to grasp the principles behind the creation of such masterpieces. As this is an introductory post, I will begin with a very simple and elegant rendering method - **ray tracing**.


**RAY TRACING**


**Situation: **

1. You have a scene filled with various objects and light sources illuminating them.

2. You have a virtual camera located at a particular position.

3. Rendering basically captures the scene as the camera would and generate an image.

**Theory:**

Ray tracing treats light as consisting of straight rays emanating from a light source and being reflected from

Ray-tracing is a rendering technique that calculates an image of a scene by simulating the way rays of light travel in the real world. In the real world, rays of light are emitted from a light source and illuminate objects. The light reflects off of the objects or passes through transparent objects. This reflected light hits the camera lens. Because the vast majority of rays never hit a camera, it would take forever to calculate all the rays. Hence, we consider only those rays that actually hit the camera by tracing the rays backwards.

[caption id="" align="alignnone" width="600"]![](http://www.ice.rwth-aachen.de/fileadmin/user_upload/forschungsprojekte/tools/GRACE/raytracing.gif) Simple Ray tracing illustration[/caption]

**Algorithm:**

Here's the basic algorithm of a ray tracer for a scene with a few objects and one fixed light source.

For every pixel of the image you wish to capture:

1. You create a ray in a direction pointing from the camera to the pixel (in the image plane). [This is done as the color of the pixel from the POV of the camera will be decided by this ray]

2. If the ray doesn't intersect any object, it means that no light ray reaches the camera in that direction and hence the pixel should be coloured black.

3. If the ray intersects an object at some point P, two cases are possible:



	
  * If the object is lit at point P, ie, point P is visible to the camera, the pixel should have the colour of the object at P.

	
  * If the object is not lit or lies in the darkness, point P is not visible to the camera, the pixel should be coloured black.


So how do we decide if point P is lit or not? Simple, we send another ray from point P to the light source. If this ray does not intersect any object (including itself), it means there is a direct light ray reaching P and hence P is lit. On the other hand, if this ray intersects another object, it means that the light from the light source to this point is blocked by another object and hence, P lies in the shadow. This particular ray that we send to check the illumination of a point is called _shadow ray_.

So now that we have a basic ray tracing algorithm ready, we can expand it further:

_**Add-on 1**_: _Multiple light sources_

In case of multiple white-light sources, we can send a shadow ray to each of them from P and if even one of them reaches a light source, it means point P is lit.

**_Add-on 2: _**_Reflection rays_

It’s also possible for objects to have very shiny and smooth reflective surfaces {mirror object in the above image}. So, to account for that, we also send a _reflection ray _from point P. To calculate the direction of reflection ray, we find the normal to the surface and the use the law of reflection which states that the angle of reflection equals the angle of incidence. Now, if the reflection ray intersects an object B at, say point Q, we again send a _shadow ray _to check if Q is illuminated or not. If it is not illuminated, then the pixel will have the colour that we obtain from the _shadow_ ray. But what if both Q and P are illuminated by light sources? In such cases, the resulting colour will be a combination of both the _shadow ray _and the _reflection ray_.

_**Add-on 3:**_** **_Refraction rays_

In a similar fashion, we can also send refraction rays based on Snell’s law of refraction and consider its contribution as well.



* * *



**That's all for now. In the coming posts of this series, I will talk about implementing the algorithm, dealing with representation of objects and rays, intersection tests, and calculating the final pixel colour based on contributions of multiple rays.**
