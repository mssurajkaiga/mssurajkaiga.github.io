---
author: mssurajkaiga
comments: true
date: 2014-08-18 06:59:55+00:00
layout: post
slug: gsoc-2014-final-summary
title: GSoC 2014 Final Summary
wordpress_id: 153
categories:
- computer graphics
- GSoC
- vispy
- visualization
tags:
- gsoc
- opengl
- vispy
---

GSoC has finally come to an end. It was an awesome experience and I would like to thank the amazing vispy developers - Luke, Eric, Almar, Cyrille and Nicolas for their guidance without which this wouldn't have been possible.

I delayed this post a bit so that I could complete a working example of a RectPolygon visual with rounded corners. Here's a sample - 

[![rectpolygon](http://mssuraj.files.wordpress.com/2014/08/rectpolygon.png?w=300)](https://mssuraj.files.wordpress.com/2014/08/rectpolygon.png)

As you can see, you can also specify a different radius of curvature for each of the four corners. The corner vertices are also generated linearly with the curvature - the more the curvature, the more the no. of vertices. Although I stumbled upon this after implementing it, here's a link which shows how the radius is defined - http://help.adobe.com/en_US/FrameMaker/8.0/help.html?content=Chap9-Graphics-Anchored-Frame_36.html

The current PR is being reviewed and I hope to get it merged by tonight before GSoC ends completely.

Here's a summary of the work completed so far:

  *  Implemented triangulation - this one is partial and is still broken. Post-GSoC I will work with my mentor Luke to wrap it up with tests.
  * Expanded the visuals library with PolygonVisual, EllipseVisual, RegularPolygonVisual
  * Added tests for each of the visuals and integrated them with the Color module by Eric
  * Modified Visuals to be reactive and added tests for the same
  * Soon to be completed - RectPolygon

Post-GSoC work:

  *  Write tests for RectPolygon
  * Wrap up triangulation
  * Expand on Cyrille's GPU ray-tracer example - https://github.com/vispy/vispy/pull/409

That's all Folks!
