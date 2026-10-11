---
layout: page
title: Hierarchical Diffusion Policy (HDP)
description: Hierarchical Diffusion Policy for Kinematics-Aware Multi-Task Robotic Manipulation (CVPR 2024).
img: assets/projects/dyson/hdp/hdp.gif
importance: 1
category: dyson
related_publications: false
---

<div class="row justify-content-center">
  <div class="col-12 text-center">
    {% include video.liquid
       path="assets/projects/dyson/hdp/hdp.mp4"
       class="img-fluid rounded z-depth-1"
       controls=true
       autoplay=false
       width="100%" %}
    <div class="caption text-center">
      Demonstration of Hierarchical Diffusion Policy (HDP) executing multi-task robotic manipulation.
    </div>
  </div>
</div>

<div class="text-center my-3">
  <a href="https://cvpr.thecvf.com/virtual/2024/poster/29288" target="_blank" rel="noopener noreferrer" class="btn btn-outline-primary btn-sm mb-1">
    <i class="fa-solid fa-file-pdf"></i> Read Paper (CVPR 2024)
  </a>
  <a href="https://arxiv.org/abs/2403.03890" target="_blank" rel="noopener noreferrer" class="btn btn-outline-primary btn-sm mb-1">
    <i class="fa-solid fa-file-lines"></i> arXiv
  </a>
  <a href="https://yusufma03.github.io/projects/hdp/" target="_blank" rel="noopener noreferrer" class="btn btn-outline-primary btn-sm mb-1">
    <i class="fa-solid fa-globe"></i> Project Website
  </a>
  <a href="https://youtu.be/f6vmzd3AKwY" target="_blank" rel="noopener noreferrer" class="btn btn-outline-primary btn-sm mb-1">
    <i class="fa-brands fa-youtube"></i> YouTube Video
  </a>
</div>

## Overview

Hierarchical Diffusion Policy (HDP) is a hierarchical imitation learning framework that decomposes complex, multi-task robotic manipulation into kinematics-aware sub-goal planning and fine-grained trajectory generation.

Standard end-to-end diffusion policies often struggle with long-horizon tasks and out-of-reach poses due to compounding error and kinematics ignorance. HDP introduces a dual-level architecture: a high-level diffusion model predicts 3D end-effector sub-goals conditioned on scene observations, while a low-level policy generates continuous, kinematically feasible trajectories. This separation ensures robust multi-task generalization and high execution success across simulated and real-world manipulation benchmarks.

---

## Summary Poster

<div class="row justify-content-center mb-4">
  <div class="col-12 text-center">
    {% include figure.liquid
       path="assets/projects/dyson/hdp/hdp_poster.svg"
       title="Hierarchical Diffusion Policy Summary Poster"
       class="img-fluid rounded z-depth-1"
       width="100%" zoomable=true %}
    <div class="caption text-center">
      Overview poster for Hierarchical Diffusion Policy (HDP).
    </div>
  </div>
</div>

---

## Authors

**Xiao Ma · Sumit Patidar · Iain Haughton · Stephen James**

---

## Publications & Resources

**Conference Paper (CVPR 2024)**

X. Ma, S. Patidar, I. Haughton and S. James, "Hierarchical Diffusion Policy for Kinematics-Aware Multi-Task Robotic Manipulation," _Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)_, 2024, pp. 18081–18090.

- [Paper (CVF Open Access)](https://openaccess.thecvf.com/content/CVPR2024/html/Ma_Hierarchical_Diffusion_Policy_for_Kinematics-Aware_Multi-Task_Robotic_Manipulation_CVPR_2024_paper.html)
- [arXiv Preprint (arXiv:2403.03890)](https://arxiv.org/abs/2403.03890)
- [Project Website](https://yusufma03.github.io/projects/hdp/)
- [Video Walkthrough](https://youtu.be/f6vmzd3AKwY)

---

## Citation

```bibtex
@inproceedings{Ma_2024_CVPR,
  author    = {Ma, Xiao and Patidar, Sumit and Haughton, Iain and James, Stephen},
  title     = {Hierarchical Diffusion Policy for Kinematics-Aware Multi-Task Robotic Manipulation},
  booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
  year      = {2024},
  pages     = {18081--18090}
}
```
