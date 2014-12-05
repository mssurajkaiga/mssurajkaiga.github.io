---
author: mssurajkaiga
comments: true
date: 2014-07-27 23:21:49+00:00
layout: post
slug: visuals-tests-gsoc-week-9
title: Visuals tests - GSoC Week 9
wordpress_id: 150
categories:
- computer graphics
- GSoC
- vispy
- visualization
tags:
- gsoc
- testing
- vispy
---

Mandatory blog post -

This week has been filled with writing tests for the Visuals.



	
  * Wrote a sort of test-bed for Visuals in the form of a TestingCanvas object.

	
  * Used it to write tests for Ellipse, Polygon and RegularPolygon visuals.

	
  * The tests would retrieve draw a visual on the canvas, retrieve an appropriate reference image from a test-data repository and would compare the two.

	
  * Minor allowances has been made to ignore small difference in the corners.

	
  * The work is available here - https://github.com/vispy/vispy/pull/327 .


Although it took a lot of iterations to get this right, it was fun to code them and learn how tests are written, how Travis- the continuous integration platform works and so on.

Next target - Make the visuals reactive!
