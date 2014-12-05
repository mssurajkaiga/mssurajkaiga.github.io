---
author: mssurajkaiga
comments: true
date: 2014-07-12 00:29:56+00:00
layout: post
slug: ellipse-regular-polygons-and-tests-gsoc-week-7
title: Ellipse, Regular polygons, and tests - GSoC Week 7
wordpress_id: 145
categories:
- computer graphics
- vispy
- visualization
tags:
- gsoc
- python
- vispy
---

I successfully passed the mid-term evaluation of GSoC. Yay! Coming to work done so far, I have implemented EllipseVisual, RegularPolygon visual, and am in the process of writing image processing based tests for them.

I implemented EllipseVisual as a generic object which can be used to draw arcs, circles as well reuse to draw regular polygons. Given a position, radii and span angles, the vertices are computed and drawn as triangle_fans. Drawing using GL_TRIANGLE_FANS made it really easy to implement the span angle part so that arcs can be easily drawn now. The code can be viewed here - https://github.com/vispy/vispy/blob/master/vispy/scene/visuals/ellipse.py . Here are some examples:

[![ellipse2](http://mssuraj.files.wordpress.com/2014/07/ellipse2.png?w=300)](https://mssuraj.files.wordpress.com/2014/07/ellipse2.png)

[![ellipse1](http://mssuraj.files.wordpress.com/2014/07/ellipse1.png?w=300)](https://mssuraj.files.wordpress.com/2014/07/ellipse1.png)

[![ellipse3](http://mssuraj.files.wordpress.com/2014/07/ellipse3.png?w=300)](https://mssuraj.files.wordpress.com/2014/07/ellipse3.png)

Similarly changing the number of segments of the triangle fan to match the number of sides resulted in regular polygons. Here's the code: https://github.com/vispy/vispy/blob/master/vispy/scene/visuals/regular_polygon.py

[![regular_polygon1](http://mssuraj.files.wordpress.com/2014/07/regular_polygon1.png?w=300)](https://mssuraj.files.wordpress.com/2014/07/regular_polygon1.png)
[![regular_polygon2](http://mssuraj.files.wordpress.com/2014/07/regular_polygon2.png?w=300)](https://mssuraj.files.wordpress.com/2014/07/regular_polygon2.png)

Currently there exists tests for none of the visuals. Tests are crucial to keep in check the visual accuracy of the visuals. Currently, I'm trying out image matching algorithms to see which one suits the need. I will publish a write-up on it once I have finished writing the tests.
