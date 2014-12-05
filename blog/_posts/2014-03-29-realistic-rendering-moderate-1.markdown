---
author: mssurajkaiga
comments: true
date: 2014-03-29 16:25:03+00:00
layout: post
slug: realistic-rendering-moderate-1
title: Realistic Rendering - [Moderate] - 1
wordpress_id: 61
categories:
- computer graphics
- rendering
tags:
- computer graphics
- physically rendering
- radiometry
- rendering
---

This series is more in line with my current studies on physically based rendering than the [[basic]](http://mssuraj.wordpress.com/2014/03/25/realistic-rendering-basic-1/) series. In this post I would like to target the basics of physically based rendering.




SO what does physically based rendering mean?




Physically based rendering uses the actual physical nature of light transport and surfaces to simulate their interaction which results in a photo-realistic image. In short, it simulates how light bounces of surfaces in a scene  as accurately as possible. To understand light transport, we first need to understand the nature of light and how it travels in nature.




Light is nothing but energy in the form of electromagnetic radiation which propagates through space. The science of measuring "how much light is there" is called _radiometry_. Hence, we will begin with some basic concepts and terminologies in radiometry which will be used in understanding and simulating light transport.




**BASIC RADIOMETRY**




**Basic Assumptions:**






	
  1. Energy is always conserved - it's neither created nor destroyed.

	
  2. No polarization - we ignore the effect of polarization for simplicity.

	
  3. No fluorescence - the behaviour of light at different wavelength's are independent of each other.


[caption id="" align="aligncenter" width="266"]![](http://www.lepla.edu.pl/en/modules/Activities/m07/images/sphere.gif) Radiometric Quantities[/caption]

**Flux (Φ):**

Radiant flux (power) is the energy per unit time that is radiated through a region of space. Its measured in J/s (Watt). Flux is the basic measurement of radiometry. All other quantities are derived from its densities. {In the above picture, both the spheres have the same flux passing through them.}

**Irradiance (E):**

Irradiance is the flux per unit area (W/m2) incident on a surface. **Radiant emittance** (or **exitance)** is the power per unit area radiated by a surface. In case the emitted flux distribution isn't constant, its useful to use irradiance at a point area dA as E = dΦ/dA. {In the above picture, the irradiance is higher on the inner sphere than the outer one as they have different areas.}

**Intensity (I):**

Intensity is the measure of flux density per unit solid angle (measured in a direction). It is mostly used with point sources—that is, emitting objects so small that we don’t care about where on the object light is coming from; just what direction it goes in.

**Radiance (L):**

Radiance is the flux density per unit area per unit solid angle (W/m2sr) (measured in a particular direction at a particular point on a surface or in space). L = d2Φ/(dA.dω). Remember that radiance considers the surface area perpendicular to the direction in question. In case a surface is inclined at an angle Θ to ω, then we consider the perpendicular component of dA, i.e. L = d2Φ/(dA.cosΘ.dω). Here, dA.cosΘ is the projected area of dA in the direction of ω.

The importance of radiance lies in the fact that it indicates how much of the power emitted by an emitting or reflecting surface will be received by an optical system looking at the surface from some angle of view. Our eyes and cameras basically respond to this quantity. Hence, the pixel values in an image is proportional to the radiance received by the camera along the pixel direction.

_[Radiance invariance: _Radiance is conserved along lines through empty space. If we look at two points in space P and Q in the direction ω pointing from one to another, then we will measure the same radiance at both the points, i.e. L(P, ω) = L(Q, ω).]

Now it's easy to derive relations among these four quantities using basic calculus. For example, irradiance at a point, E can be calculated by the following, where Li is the arriving radiance as seen along the direction ωi .

[caption id="" align="aligncenter" width="390"]![](http://escience.anu.edu.au/lecture/cg/GlobalIllumination/Image/Irradiance.gif) Irradiance from radiance[/caption]



To make it easier to represent the relations between various quantities, we can also hide the cosine terms by grouping (cosΘ.dω). We call this the "projected solid angle" measure.



Now that we have the basic quantities, we can describe the interaction of light with objects using them. I will start by describing one of the fundamental concepts in describing the reflection of lights on surfaces - BRDF.


**BRDF (Bidirectional Reflectance Distribution Function)**




Consider a surface with light incident on it at a particular point. Obviously, light is radiated by the surface at that point as well. We would like to describe the relation between the amount of light radiated from this point in a particular direction and the light incident on it. This is the purpose of BRDF.




[caption id="attachment_80" align="aligncenter" width="284"][![Bidirectional Reflectance Distribution Function](http://mssuraj.files.wordpress.com/2014/03/ilgri_brdf.jpg?w=284)](http://mssuraj.files.wordpress.com/2014/03/ilgri_brdf.jpg) Bidirectional Reflectance Distribution Function[/caption]



To describe it mathematically, let's assume that light is incident at point P on a surface along direction ωi. Let the direction along which we require the amount of light radiated be ωr. We consider the portion of light in an infinitesimal solid angle dωi around ωi. If the radiance along ωi is Li(P, ωi), then the infinitesimal irradiance on the surface at P is given by


dE(P, ωi) = L(P, ωi) cosΘ dωi




We also assume that the surface scatters the light resulting in a distribution of reflected radiances over various outgoing directions. Let the infinitesimal amount of light radiated in the direction wr be represented as dLr(P, ωr). Then the BRDF is the ratio between the reflected radiance to the incident irradiance.




**fr(P, ωr, ωi) = dLr(P, ωr) / dE(P, ωi)**




**Properties of BRDF:**






	
  1. Reciprocity: BRDFs are invariant with respect to swapping their arguments i.e., fr(P, ω1, ω2) = fr(P, ω2, ω1).

	
  2. Energy Conservation: The total energy of light reflected must be less than or equal to the energy of the incident light. For all directions ωr,




[![equation](http://mssuraj.files.wordpress.com/2014/03/equation.gif)](http://mssuraj.files.wordpress.com/2014/03/equation.gif)




Similarly, we can also describe **BTDF** - _Bidirectional Transmittance Distribution Function_. The BTDF is identical to BRDF in definition except that the direction vectors do not lie on the same side of the surface. Also, BTDF does not obey reciprocity.




The BRDF and BTDF are combined together as one function **f(P, ωr, ωi)** to give the **BSDF** - _Bidirectional Scattering Distribution Function. _Using this definition of BSDF, we have




[![](http://latex.codecogs.com/gif.latex?\&space;L_o(P,&space;\omega_o)&space;=&space;\int_{S^2}&space;L_i(P,&space;\omega_i).f(P,&space;\omega_o,&space;\omega_i).\left&space;|cos\theta_i&space;\right&space;|d\omega_i)](http://www.codecogs.com/eqnedit.php?latex=\&space;L_o(P,&space;\omega_o)&space;=&space;\int_{S^2}&space;L_i(P,&space;\omega_i).f(P,&space;\omega_o,&space;\omega_i).\left&space;|cos\theta_i&space;\right&space;|d\omega_i)




This is a fundamental equation in rendering called the _scattering equation. _Here, Lo represents the outward radiance at P along ωo. Note that instead of fr we have simply f, which is the BSDF.






* * *



**That’s all for now. There are some stuff like BSSRDF, phase function and rendering equation that I haven't discussed. I will explain them briefly in the coming posts of this series. I will also discuss Monte Carlo integration, BRDF models and path tracing along the way.**
