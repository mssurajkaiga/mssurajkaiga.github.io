---
author: mssurajkaiga
comments: true
date: 2014-06-01 12:42:15+00:00
layout: post
slug: constrained-delaunay-triangulation
title: Constrained Delaunay Triangulation - GSoC Week 2
wordpress_id: 119
categories:
- computer graphics
- GSoC
- vispy
tags:
- computer graphics
- delaunay
- gsoc
- triangulation
- vispy
---

My primary focus during GSoC is on implementing visuals like PolygonVisuals, EllipseVisuals using the existing visuals layer. But a major need for these visuals is triangulation - splitting these primitives like polygons, ellipses into triangles. **Every object can be split into triangles but a triangle cannot be split into anything else than triangles.** Because of this, drawing triangles is a lot simpler than drawing polygons of higher order; less things to deal with. Hence, triangulation!

Triangulation is very important to vispy as there is no support for it in OpenGL ES 2.0 (which is used by vispy). So, I will be implementing it as part of a new module in vispy, vispy.geometry.

[![sphere_grid](http://mssuraj.files.wordpress.com/2014/06/sphere_grid.png?w=300)](https://mssuraj.files.wordpress.com/2014/06/sphere_grid.png)



Most of the discussions with my mentors Luke, Cyrille, Eric and Almar on vispy.geometry are available here [https://github.com/vispy/vispy/issues/194](https://github.com/vispy/vispy/issues/194) .

To begin with, I will implement a simple version of  **Sweep‐line algorithm for constrained Delaunay triangulation **by Domiter and Zalik - http://www.tandfonline.com/doi/abs/10.1080/13658810701492241#.U4sVxB837Pk . The starting code with visual debugging has already been written by my awesome mentor Luke , so that makes my work easier :)

I believe that a bit of explanation regarding triangulation is in order. So here goes - A given set of points (possibly representing a polygon) can be triangulated in a number of ways.  Delaunay triangulation is one of them that maximize the minimum angle of all the angles of the triangles in the triangulation; they tend to avoid skinny triangles. The basic rule of Delaunay triangulation is that no point should lie inside the circumcircle of a triangle. Constrained Delaunay triangulation just adds few more constraints to the same.

[![Reduction of artifacts in CT attenuation corrected PET data caus](http://mssuraj.files.wordpress.com/2014/06/medium_259_2011_1900_fig2_html.jpg?w=284)](https://mssuraj.files.wordpress.com/2014/06/medium_259_2011_1900_fig2_html.jpg)

So, the things to do by next week:

1. Finish work on Delaunay triangulation

2. Start trying out the existing visual classes and examples

PS: Although my work is going bit slower than expected, I expect to pick-up pace once the triangulation code is completed.
