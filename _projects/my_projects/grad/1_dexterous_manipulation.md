---
layout: page
title: "In-Hand Cube Reconfiguration: Simplified"
description: Gravity-driven in-hand manipulation through constraint exploitation and wrist movements.
img: assets/img/publication_preview/rh3_spin.gif
importance: 1
category: grad
related_publications: false
---

<div class="row justify-content-md-center">

  <div class="col-sm-5 mt-4 mt-md-0">
    {% include video.liquid
       path="assets/projects/grad/dexterous_manipulation/rh3_perspective.mp4"
       class="img-fluid rounded z-depth-1"
       controls=true
       autoplay=false %}
    <div class="caption text-center">
      <strong>Gravity in Disguise!</strong><br>
      In-hand manipulation using gravity and wrist movements.
    </div>
  </div>

  <div class="col-sm-7 mt-4 mt-md-0">
    {% include video.liquid
       path="https://www.youtube.com/embed/7IIQrVgDE2E"
       class="rounded z-depth-1" %}
    <div class="caption text-center">
      Spelling demonstration using an open-loop sequence of motion primitives.
    </div>
  </div>

</div>

<div class="text-center my-3">
  <a href="https://ieeexplore.ieee.org/document/10341521" target="_blank" rel="noopener noreferrer" class="btn btn-outline-primary btn-sm mb-1">
    <i class="fa-solid fa-file-pdf"></i> Read Paper (IEEE Xplore)
  </a>
  <a href="https://rbo.gitlab-pages.tu-berlin.de/robotics/simpleIHM/" target="_blank" rel="noopener noreferrer" class="btn btn-outline-primary btn-sm mb-1">
    <i class="fa-solid fa-globe"></i> Project Website
  </a>
  <a href="https://www.static.tu.berlin/fileadmin/www/10002220/Theses/sumit_ma.pdf" target="_blank" rel="noopener noreferrer" class="btn btn-outline-primary btn-sm mb-1">
    <i class="fa-solid fa-graduation-cap"></i> Master's Thesis
  </a>
  <a href="https://spectrum.ieee.org/video-friday-squishable-bugbot" target="_blank" rel="noopener noreferrer" class="btn btn-outline-primary btn-sm mb-1">
    <i class="fa-solid fa-newspaper"></i> IEEE Spectrum Feature
  </a>
</div>

## Overview

We present a simple, constraint-based approach to in-hand cube reconfiguration using gravity and inertial forces as the sole actuation sources. By exploiting contact constraints through wrist movements, the hand acts primarily as a constraint reconfigurator, simplifying planning and control.

We demonstrate robust reconfiguration of a cube across all 24 possible orientations using a sequence of simple open-loop motion primitives, highlighting the potential of classical planning and environmental constraints for dexterous manipulation without complex finger actuation.

---

## Key Contributions

- **Gravity-Driven Constraint Exploitation:** Formulated a manipulation paradigm that leverages gravity and inertial dynamics as primary actuation sources, shifting the robotic hand from an active actuator to an adaptable contact constraint during manipulation.
- **Open-Loop Motion Primitives:** Designed 5 robust primitive motions (spin, roll, shift left, shift right, and shift back) executed entirely via arm/wrist trajectories without requiring active finger joint articulation.
- **Complete In-Hand Reconfiguration:** Developed a high-level graph-search planning routine that systematically sequences primitives to achieve all 24 possible spatial $SO(3)$ orientations of a cube.
- **Physical Robotic Validation:** Experimentally validated the framework on an anthropomorphic soft hand (RBO Hand 3) mounted on a Franka Emika Panda arm, demonstrating sustained multi-step reconfigurations and an autonomous spelling task.

---

## Method & Motion Primitives

<div class="row justify-content-md-center">

  <div class="col-md-4 col-12 text-center mb-3">
    {% include figure.liquid
       path="assets/projects/grad/dexterous_manipulation/fig1_sequence.png"
       width="100%"
       class="img-fluid rounded z-depth-1"
       zoomable=true %}
    <div class="caption">
      <strong>Figure 1: Cube reconfiguration sequence.</strong>
      A sequence of motion primitives transforms the initial cube configuration into the desired orientation.
    </div>
  </div>

  <div class="col-md-4 col-12 text-center mb-3">
    {% include figure.liquid
       path="assets/projects/grad/dexterous_manipulation/fig2_primitives.png"
       width="100%"
       class="img-fluid rounded z-depth-1"
       zoomable=true %}
    <div class="caption">
      <strong>Figure 2: Motion primitives.</strong>
      Five primitives—spin, shift left, shift right, shift back, and roll—exploit contact constraints to reorient the cube.
    </div>
  </div>

  <div class="col-md-4 col-12 text-center mb-3">
    {% include figure.liquid
       path="assets/projects/grad/dexterous_manipulation/fig3_routine.png"
       width="100%"
       class="img-fluid rounded z-depth-1"
       zoomable=true %}
    <div class="caption">
      <strong>Figure 3: Motion primitive sequencing.</strong>
      A high-level routine combines motion primitives to execute a cube reconfiguration task.
    </div>
  </div>

</div>

The approach decomposes cube reconfiguration into a sequence of simple motion primitives that exploit contact constraints between the hand and the object. By leveraging gravity and inertial forces through wrist movements, these primitives enable the cube to spin, roll, and shift within the hand. A high-level routine combines them to achieve the desired configuration, reducing the complexity of planning and control while retaining robust manipulation capabilities.

---

## Extended Manipulation Sequences

<div class="row justify-content-md-center">
  <div class="col-md-10 text-center">
    {% include video.liquid
       path="https://www.youtube.com/embed/AxMmgoZYe1k"
       class="rounded z-depth-1" %}
    <div class="caption text-center">
      <strong>Long manipulation sequence:</strong> Continuous execution of open-loop manipulation primitives demonstrating sustained stability and multi-step in-hand cube reconfiguration.
    </div>
  </div>
</div>

---

## Technical Highlights

- **Robotic Platform:** RBO Hand 3 (compliant anthropomorphic soft hand) mounted on a Franka Emika Panda robotic arm
- **Actuation Principle:** Gravity and wrist inertial forces (zero active finger movement during manipulation)
- **Reconfiguration Space:** Complete coverage across all 24 orientations of a cube in 3D space
- **Motion Primitives:** 5 open-loop primitives (spin, roll, shift left, shift right, shift back)
- **Planning Paradigm:** High-level graph-search primitive sequencing without real-time tactile or vision feedback loops
- **Validation:** Multi-primitive spelling demonstrations and long sustained reconfiguration sequences

---

## Publications & Resources

**Conference Paper (IROS 2023)**

S. Patidar, A. Sieler and O. Brock, "In-Hand Cube Reconfiguration: Simplified," _2023 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS)_, Detroit, MI, USA, 2023, pp. 8751–8756.

- [Read Paper (IEEE Xplore)](https://ieeexplore.ieee.org/document/10341521)
- [Project Website](https://rbo.gitlab-pages.tu-berlin.de/robotics/simpleIHM/)

**Master's Thesis**

S. Patidar, "In-Hand Manipulation via Constraint Exploitation and Wrist-Movements," Master's Thesis, Technical University of Berlin, 2022.

- [Read Thesis (PDF)](https://www.static.tu.berlin/fileadmin/www/10002220/Theses/sumit_ma.pdf)

**Media Coverage**

- [IEEE Spectrum – Video Friday](https://spectrum.ieee.org/video-friday-squishable-bugbot)

<div class="row mt-2">
  <div class="col-sm-4">
    {% include figure.liquid
       path="assets/projects/grad/dexterous_manipulation/ieee_spectrum.png"
       title="IEEE Spectrum Video Friday Feature"
       class="img-fluid rounded z-depth-1"
       zoomable=true %}
  </div>
</div>

---

## Citation

If you find this work useful in your research, please cite our IROS paper:

```bibtex
@inproceedings{patidar2023inhand,
  author    = {Patidar, Sumit and Sieler, Adrian and Brock, Oliver},
  title     = {In-Hand Cube Reconfiguration: Simplified},
  booktitle = {2023 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS)},
  year      = {2023},
  pages     = {8751--8756},
  doi       = {10.1109/IROS55552.2023.10341521}
}
```

---

## Acknowledgements

This work was carried out at the Robotics and Biology Laboratory, Technical University of Berlin, as part of my master's thesis. I am grateful to [Adrian Sieler](https://scholar.google.com/citations?user=DaQiBfMAAAAJ&hl=de) for his mentorship and to [Prof. Oliver Brock](https://www.tu.berlin/en/robotics/about-rbo/prof-dr-oliver-brock) for supervising this work. Their guidance and the research environment at the lab were instrumental in making this project possible.
