---
layout: page
title: In-Hand Manipulation - Simplified
description: In-Hand Manipulaton via Constraint Exploitation and Wrist-Movements🤌
img: assets/img/publication_preview/rh3_spin.gif
importance: 1
category: grad
---

<div class="row justify-content-sm-center">
{% include video.liquid path="https://www.youtube.com/embed/7IIQrVgDE2E?si=i54MShCxrh3y6xcZ" class="rounded z-depth-1" width="640px" height="360px" %}
</div>
<div class="caption">
    Spelling demonstration using an open-loop sequence of motion primitives.
</div>

This master’s thesis represents the culmination of my work at the Robotics and Biology Laboratory at the Technical University of Berlin, where I have had the privilege of exploring the fascinating intersection of robotics and biology. I am deeply grateful to Adrian Sieler (PhD), whose mentorship and insights have been invaluable in navigating the challenges and breakthroughs of this project. My sincere thanks also go to Prof. Oliver Brock, whose guidance as my thesis supervisor has been instrumental in shaping this research journey. This work is a testament to their support and the inspiring environment fostered at the lab.

## Introduction

We present in-hand manipulation skills using gravity and inertial forces as the only actuation sources on a dexterous, compliant, anthropomorphic hand. Gravity, a flexible actuation source, can be used to exploit all constraints in the surrounding of an object. We leverage gravity and inertial forces by employing
wrist motions to exploit the constraints provided by the hand. Exploiting these constraints leads to a reconfiguration of an object within the hand. In this work, we tackle the problem of cube reconĄguration to investigate the possibilities of purely wrist-based manipulation. For this, we limit the actuation
sources to gravity and inertial forces and use the hand purely as a constraint reconfigurator. This reduces the action space for manipulation and simpliflies the required control and modeling. We decompose the manipulation task
into a sequence of gravity-based constraint-exploitations. Our first approach uses hand-crafted open-loop skills to manipulate diverse objects. The second approach incorporates object state feedback to account for skill failures, variation in object placements, and human perturbations for robust manipulation of a cube. Using both approaches, we robustly manipulate a cube to any of its 24 configurations. Our results show we can achieve versatile manipulation by
constraint configuration and exploitation through wrist movements.

## Curious to Dive Deeper?

Eager to explore what we uncovered? Discover the full thesis, our presentation at IROS, and a detailed project overview below:

1. [Thesis](https://www.static.tu.berlin/fileadmin/www/10002220/Theses/sumit_ma.pdf)
2. [IROS Paper](https://ieeexplore.ieee.org/document/10341521)
3. [Project website](https://rbo.gitlab-pages.tu-berlin.de/robotics/simpleIHM/)
4. [IEEE Video Friday](https://spectrum.ieee.org/video-friday-squishable-bugbot)
