---
author: mssurajkaiga
comments: true
date: 2014-06-21 20:19:38+00:00
layout: post
slug: polygon-visuals-gsoc-mid-term
title: Polygon Visuals - GSoC Mid-term
wordpress_id: 96
categories:
- computer graphics
- GSoC
- vispy
- visualization
tags:
- geometry
- gsoc
- opengl
- vispy
- visualization
---

GSoC midterm is almost here and as expected, I have picked up good pace. Most of the triangulation is complete, a bit of polishing remains. I have also refactored it to be part of geometry module. I have been testing and fixing bugs on my implementation by testing it out on different data. One thing I have realised is that it doesn't work on self-intersecting polygons. It is not supported by the algorithm itself and will probably require the use of a clipping library before triangulation.

An example of triangulation (without recursive legalization):

[![triangulation1](http://mssuraj.files.wordpress.com/2014/06/triangulation1.png?w=300)](https://mssuraj.files.wordpress.com/2014/06/triangulation1.png)

I have also implemented PolygonVisual in vispy with triangulation and borders. Unexpectedly, at least for me, this also happens to be the first compound visual being added to vispy. Good thing that MeshVisual and LineVisual were already implemented which form the basis of this. I also added a mode attribute so that the LineVisual can be drawn using GL_LINES or GL_LINE_STRIP (whichever format the data is provided in).

As of now, I am using Delaunay triangulation from scipy.spatial in PolygonVisual till the vispy.geometry.triangulation is tested and fixed completely. Once done, it will become part of the geometry module.

Here are few example of PolygonVisual:

[![polygonvisual1](http://mssuraj.files.wordpress.com/2014/06/polygonvisual1.png?w=300)](https://mssuraj.files.wordpress.com/2014/06/polygonvisual1.png) [![polygonvisual2](http://mssuraj.files.wordpress.com/2014/06/polygonvisual2.png?w=300)](https://mssuraj.files.wordpress.com/2014/06/polygonvisual2.png)

Although this wasn't in my proposal, on discussing with my mentor Luke, I have also appended to the geometry module data handling features for polygon so that the visuals module remains uncluttered.  Next week, I will add triangulation tests and more features geometry module like bounding rectangle. Till then, cheers!
