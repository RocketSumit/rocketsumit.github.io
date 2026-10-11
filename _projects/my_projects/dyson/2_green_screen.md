---
layout: page
title: Green Screen Augmentation
description: Green Screen Augmentation Enables Scene Generalisation in Robotic Manipulation (arXiv 2024).
img: assets/projects/dyson/green_screen/greenaug.gif
importance: 2
category: dyson
related_publications: false
---

<div class="row justify-content-center">
  <div class="col-12 text-center">
    {% include video.liquid
       path="assets/projects/dyson/green_screen/green_screen.mp4"
       class="img-fluid rounded z-depth-1"
       controls=true
       autoplay=false
       width="100%" %}
    <div class="caption text-center">
      Demonstration of Green Screen Augmentation for zero-shot scene generalization in manipulation.
    </div>
  </div>
</div>

<div class="text-center my-3">
  <a href="https://arxiv.org/abs/2407.07868" target="_blank" rel="noopener noreferrer" class="btn btn-outline-primary btn-sm mb-1">
    <i class="fa-solid fa-file-pdf"></i> Read Paper (arXiv)
  </a>
  <a href="https://greenaug.github.io/" target="_blank" rel="noopener noreferrer" class="btn btn-outline-primary btn-sm mb-1">
    <i class="fa-solid fa-globe"></i> Project Website
  </a>
  <a href="https://youtu.be/KWG9JUkUAxQ" target="_blank" rel="noopener noreferrer" class="btn btn-outline-primary btn-sm mb-1">
    <i class="fa-brands fa-youtube"></i> YouTube Video
  </a>
</div>

## Overview

Green Screen Augmentation is a data augmentation framework designed to achieve robust visual scene generalisation for robot manipulation policies without requiring expensive multi-environment data collection.

Vision-based policies frequently overfit to visual background textures, table surfaces, and ambient lighting in their training setup. Green Screen Augmentation addresses this by segmenting the robot and task-relevant objects from the background using green-screen-inspired chroma-keying and synthetic background compositing. By training models with diverse background augmentations, the learned policies exhibit zero-shot generalisation to novel visual backgrounds, lighting conditions, and cluttered tabletop distractors in the real world.

---

## Summary Poster

<div class="row justify-content-center mb-4">
  <div class="col-12 text-center">
    {% include figure.liquid
       path="assets/projects/dyson/green_screen/green_screen_poster.svg"
       title="Green Screen Augmentation Summary Poster"
       class="img-fluid rounded z-depth-1"
       width="100%" zoomable=true %}
    <div class="caption text-center">
      Overview poster for Green Screen Augmentation.
    </div>
  </div>
</div>

---

## Authors

**Eugene Teoh · Sumit Patidar · Xiao Ma · Stephen James**

---

## Publications & Resources

**Preprint (2024)**

E. Teoh, S. Patidar, X. Ma and S. James, "Green Screen Augmentation Enables Scene Generalisation in Robotic Manipulation," _arXiv preprint arXiv:2407.07868_, 2024.

- [arXiv Preprint (arXiv:2407.07868)](https://arxiv.org/abs/2407.07868)
- [Project Website](https://greenaug.github.io/)
- [Video Demonstration](https://youtu.be/KWG9JUkUAxQ)

---

## Citation

```bibtex
@article{teoh2024green,
  author  = {Teoh, Eugene and Patidar, Sumit and Ma, Xiao and James, Stephen},
  title   = {Green Screen Augmentation Enables Scene Generalisation in Robotic Manipulation},
  journal = {arXiv preprint arXiv:2407.07868},
  year    = {2024}
}
```
