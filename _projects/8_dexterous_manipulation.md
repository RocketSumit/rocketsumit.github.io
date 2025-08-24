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

- [Abstract](#abstract)
- [Curious to Dive Deeper?](#curious-to-dive-deeper)

## Abstract

We present in-hand manipulation skills using gravity and inertial forces as the only actuation sources on a dexterous, compliant, anthropomorphic hand. Gravity, a flexible actuation source, can be used to exploit all constraints in the surrounding of an object. We leverage gravity and inertial forces by employing
wrist motions to exploit the constraints provided by the hand. Exploiting these constraints leads to a reconfiguration of an object within the hand. In this work, we tackle the problem of cube reconĄguration to investigate the possibilities of purely wrist-based manipulation. For this, we limit the actuation
sources to gravity and inertial forces and use the hand purely as a constraint reconfigurator. This reduces the action space for manipulation and simpliflies the required control and modeling. We decompose the manipulation task
into a sequence of gravity-based constraint-exploitations. Our first approach uses hand-crafted open-loop skills to manipulate diverse objects. The second approach incorporates object state feedback to account for skill failures, variation in object placements, and human perturbations for robust manipulation of a cube. Using both approaches, we robustly manipulate a cube to any of its 24 configurations. Our results show we can achieve versatile manipulation by
constraint configuration and exploitation through wrist movements.

## Curious to Dive Deeper?

Eager to explore what we uncovered? Discover the full thesis, our presentation at IROS, and a detailed project overview below:

1. [In-Hand Manipulation via Constraint Exploitation and Wrist-Movements](https://www.static.tu.berlin/fileadmin/www/10002220/Theses/sumit_ma.pdf). Master Thesis. Available at: https://www.static.tu.berlin/fileadmin/www/10002220/Theses/sumit_ma.pdf (Accessed: 12 December 2024).

2. S. Patidar, A. Sieler and O. Brock, "In-Hand Cube Reconfiguration: Simplified," 2023 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS), Detroit, MI, USA, 2023, pp. 8751-8756, doi: 10.1109/IROS55552.2023.10341521, url: [https://ieeexplore.ieee.org/document/10341521](https://ieeexplore.ieee.org/document/10341521) (Accessed: 12 December 2024).

3. [simpleIHM](https://rbo.gitlab-pages.tu-berlin.de/robotics/simpleIHM/). Project Website. Available at: https://rbo.gitlab-pages.tu-berlin.de/robotics/simpleIHM/ (Accessed: 12 December 2024).

4. [Video Friday](https://spectrum.ieee.org/video-friday-squishable-bugbot). IEEE Spectrum. Available at: https://spectrum.ieee.org/video-friday-squishable-bugbot (Accessed: 12 December 2024).
