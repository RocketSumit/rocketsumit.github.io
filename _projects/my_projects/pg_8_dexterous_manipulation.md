---
layout: page
title: "In-Hand Cube Reconfiguration: Simplified"
description: Gravity-driven in-hand manipulation through constraint exploitation and wrist movements.
img: assets/img/publication_preview/rh3_spin.gif
importance: 1
category: grad
---

<div class="row justify-content-md-center">

  <div class="col-sm-6 mt-4 mt-md-0">
    {% include video.liquid
       path="assets/projects/inhand_manipulation_rh3/rh3_perspective.mp4"
       class="img-fluid rounded z-depth-1"
       controls=true
       autoplay=false %}
    <div class="caption text-center">
      <strong>Gravity in Disguise!</strong><br>
      In-hand manipulation using gravity and wrist movements.
    </div>
  </div>

  <div class="col-sm-6 mt-4 mt-md-0">
    {% include video.liquid
       path="https://www.youtube.com/embed/7IIQrVgDE2E"
       class="rounded z-depth-1"
       width="100%"
       height="360px" %}
    <div class="caption text-center">
      Spelling demonstration using an open-loop sequence
      of motion primitives.
    </div>
  </div>

</div>

## Overview

We present a simple, constraint-based approach to in-hand
cube reconfiguration using gravity and inertial forces as
the sole actuation sources. By exploiting contact constraints
through wrist movements, the hand acts primarily as a
constraint reconfigurator, simplifying planning and control.
We demonstrate robust reconfiguration of a cube across all
24 possible orientations using a sequence of simple motion
primitives, highlighting the potential of classical planning
and environmental constraints for dexterous manipulation.

## Method

<div class="row justify-content-md-center">

  <div class="col-md-4 col-12 text-center mb-3">
    {% include figure.liquid
       path="assets/projects/inhand_manipulation_rh3/fig1_sequence.png"
       width="100%"
       class="img-fluid rounded z-depth-1" %}
    <div class="caption">
      <strong>Figure 1: Cube reconfiguration sequence.</strong>
      A sequence of motion primitives transforms the initial
      cube configuration into the desired orientation.
    </div>
  </div>

  <div class="col-md-4 col-12 text-center mb-3">
    {% include figure.liquid
       path="assets/projects/inhand_manipulation_rh3/fig2_primitives.png"
       width="100%"
       class="img-fluid rounded z-depth-1" %}
    <div class="caption">
      <strong>Figure 2: Motion primitives.</strong>
      Five primitives—spin, shift left, shift right, shift
      back, and roll—exploit contact constraints to
      reorient the cube.
    </div>
  </div>

  <div class="col-md-4 col-12 text-center mb-3">
    {% include figure.liquid
       path="assets/projects/inhand_manipulation_rh3/fig3_routine.png"
       width="100%"
       class="img-fluid rounded z-depth-1" %}
    <div class="caption">
      <strong>Figure 3: Motion primitive sequencing.</strong>
      A high-level routine combines motion primitives
      to execute a cube reconfiguration task.
    </div>
  </div>

</div>

The approach decomposes cube reconfiguration into a sequence
of simple motion primitives that exploit contact constraints
between the hand and the object. By leveraging gravity and
inertial forces through wrist movements, these primitives
enable the cube to spin, roll, and shift within the hand.
A high-level routine combines them to achieve the desired
configuration, reducing the complexity of planning and
control while retaining robust manipulation capabilities.

## Acknowledgements

This work was carried out at the Robotics and Biology
Laboratory, Technical University of Berlin, as part of my
master's thesis. I am grateful to
[Adrian Sieler](https://scholar.google.com/citations?user=DaQiBfMAAAAJ&hl=de)
for his mentorship and to [Prof. Oliver Brock](https://www.tu.berlin/en/robotics/about-rbo/prof-dr-oliver-brock) for supervising
this work. Their guidance and the research environment at
the lab were instrumental in making this project possible.

## Publications & Resources

**Conference paper**

S. Patidar, A. Sieler and O. Brock,
"In-Hand Cube Reconfiguration: Simplified,"
_2023 IEEE/RSJ International Conference on Intelligent
Robots and Systems (IROS)_, Detroit, MI, USA,
2023, pp. 8751–8756.

- [Read the paper (IEEE Xplore)](https://ieeexplore.ieee.org/document/10341521)
- [Project website](https://rbo.gitlab-pages.tu-berlin.de/robotics/simpleIHM/)

**Master's thesis**

[In-Hand Manipulation via Constraint Exploitation and
Wrist-Movements](https://www.static.tu.berlin/fileadmin/www/10002220/Theses/sumit_ma.pdf)

**Related coverage**

[IEEE Spectrum – Video Friday](https://spectrum.ieee.org/video-friday-squishable-bugbot)
