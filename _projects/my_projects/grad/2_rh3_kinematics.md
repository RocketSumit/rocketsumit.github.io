---
layout: page
title: Soft Hand Kinematics
description: Learning forward and inverse kinematics of the compliant RBO Hand 3 for control and visualization.
img: assets/projects/grad/rh3_kinematics/rh3.gif
importance: 2
category: grad
related_publications: false
---

<div class="row justify-content-center">
  <div class="col-sm-4 text-center">
    {% include figure.liquid
       path="assets/projects/grad/rh3_kinematics/rh3.gif"
       title="RBO Hand 3 compliance animation"
       class="img-fluid rounded z-depth-1"
       width="100%" %}
    <div class="caption text-center">
      The compliant RBO Hand 3: Actuating soft pneumatic continuum fingers and palm bellows.
    </div>
  </div>
</div>

<div class="text-center my-3">
  <a href="{{ '/assets/projects/grad/rh3_kinematics/rh3_kinematics_technical_report.pdf' | relative_url }}" target="_blank" rel="noopener noreferrer" class="btn btn-outline-primary btn-sm">
    <i class="fa-solid fa-file-pdf"></i> Read Technical Report (PDF)
  </a>
</div>

## Overview

The **RBO Hand 3** is an anthropomorphic soft robotic hand developed at the Robotics and Biology Laboratory (RBO), Technical University of Berlin. Designed for robust dexterous grasping, its fingers are soft silicone continuum pneumatic actuators that undergo continuous elastic deformations with virtually infinite mechanical degrees of freedom.

Unlike rigid-link robots, modeling soft fingers with analytical forward and inverse kinematics is notoriously difficult, while finite-element methods (FEM) are too computationally intensive for real-time control.

This project introduces an efficient, **hybrid data-driven and analytical kinematic modeling approach**. We model the non-linear continuum bending of the compliant fingers using shallow neural networks and $K$-NN regression, and couple them with analytical Denavit-Hartenberg (DH) kinematic transformations for the rigid-like revolute palm and thumb bellows.

---

## Key Contributions

- **Hybrid Kinematic Framework:** Formulated a modular architecture coupling data-driven continuum compliance models with analytical revolute link transformations, avoiding the prohibitive cost of whole-hand 3D grid data collection.
- **MoCap Data Collection & Preprocessing:** Captured high-precision motion capture (MoCap) trajectories tracking 3D fingertip positions and joint angles across multiple airmass inflation/deflation cycles.
- **Forward & Inverse Model Learning:** Trained feedforward neural networks for finger compliance and inverse mapping, alongside distance-weighted $K$-NN regression ($k=12$) over a 76-million point workspace for the 4-DOF thumb chain.
- **Kinematic Simulation & Kapandji Test:** Built the full hand model in ROS/RViz and validated reachability and thumb opposability through the clinical Kapandji test.
- **Mobile Application Development:** Built a cross-platform **Flutter** application for real-time forward and inverse kinematic prediction and interactive 3D fingertip visualization.

---

## Kinematic Formulations

Let $\mathbf{X} = [x, y, z]^T \in \mathbb{R}^3$ denote the Cartesian fingertip position in the reference frame, $\boldsymbol{\mu}$ denote the pneumatic airmass vector (mg) injected into the finger chambers, and $\boldsymbol{\theta}$ represent the actuator joint angles on the palm.

### 1. Index and Middle Fingers (Decoupled Compliance)

The index and middle fingers mount directly to the palm base with no intermediate revolute actuators. Their kinematics depend solely on the internal airmass levels $\boldsymbol{\mu} = [\mu_1, \mu_2]^T$:

$$\mathbf{X} = c_i(\boldsymbol{\mu}), \quad \forall i \in \{\text{index, middle}\}$$

$$\boldsymbol{\mu} = c_i^{-1}(\mathbf{X}), \quad \forall i \in \{\text{index, middle}\}$$

where $c_i$ is a learned forward neural network model and $c_i^{-1}$ is the inverse model mapping desired Cartesian position back to required airmass.

### 2. Ring and Little Fingers (Coupled Palm Scaffold)

The ring and little fingers are mounted onto a movable palm scaffold that provides palm cupping via revolute joint angle $\theta_{\text{palm\_scaffold}}$. The forward kinematics couples the finger's compliant base position with the palm transformation matrix $\mathbf{T}$:

$$\mathbf{X} = \mathbf{T}(\theta_{\text{palm\_scaffold}}) \cdot c_i(\boldsymbol{\mu}), \quad \forall i \in \{\text{ring, little}\}$$

The inverse kinematics predicts the full configuration vector $\boldsymbol{\theta} = [\boldsymbol{\mu}, \theta_{\text{palm\_scaffold}}]^T$ from the target Cartesian position:

$$\boldsymbol{\theta} = f_i^{-1}(\mathbf{X}), \quad \forall i \in \{\text{ring, little}\}$$

### 3. Thumb Kinematic Chain (4-DOF Multi-Joint Coupling)

The thumb comprises three pneumatic bellow actuators on the palm ($T_1, T_2, T_3$) acting as revolute joints, followed by a single-compartment continuum bending finger:

$$\mathbf{X} = \mathbf{T}(\theta_{T_1}, \theta_{T_2}, \theta_{T_3}) \cdot c_{\text{thumb}}(\mu)$$

where $\mathbf{T}(\theta_{T_1}, \theta_{T_2}, \theta_{T_3})$ is computed using Denavit-Hartenberg parameters from the thumb kinematic chain.

Because the resulting workspace contains over 76 million potential configurations, the inverse kinematics is learned using distance-weighted $K$-Nearest Neighbors ($K$-NN) regression ($k=12$):

$$\boldsymbol{\theta} = f_{\text{thumb}}^{-1}(\mathbf{X}) = [\mu, \theta_{T_1}, \theta_{T_2}, \theta_{T_3}]^T$$

---

## Workspace Analysis & Modeling

<div class="row justify-content-center align-items-center mb-3">
  <div class="col-md-6 text-center mb-3 mb-md-0">
    {% include figure.liquid
       path="assets/projects/grad/rh3_kinematics/rh3_components.png"
       title="RBO Hand 3 Structure"
       class="img-fluid rounded z-depth-1"
       width="100%" zoomable=true %}
    <div class="caption text-center">
      <strong>RBO Hand 3 Architecture:</strong> Four 2-compartment continuum fingers, single-compartment thumb, palm scaffold actuator, and T1–T3 thumb positioning bellows.
    </div>
  </div>
  <div class="col-md-6 text-center">
    {% include figure.liquid
       path="assets/projects/grad/rh3_kinematics/all_finger_heatmap.png"
       title="Reachable workspace of all fingers"
       class="img-fluid rounded z-depth-1"
       width="100%" zoomable=true %}
    <div class="caption text-center">
      <strong>Finger Reachable Workspace:</strong> 3D MoCap point clouds of fingertip trajectories generated during cyclic pneumatic inflation/deflation.
    </div>
  </div>
</div>

<div class="row justify-content-center align-items-center mb-3">
  <div class="col-md-6 text-center mb-3 mb-md-0">
    {% include figure.liquid
       path="assets/projects/grad/rh3_kinematics/ring_little_combined_workspace.png"
       title="Ring and little finger workspace"
       class="img-fluid rounded z-depth-1"
       width="100%" zoomable=true %}
    <div class="caption text-center">
      <strong>Ring & Little Finger Workspace:</strong> Combined reachable volume resulting from finger inflation coupled with palm scaffold rotation.
    </div>
  </div>
  <div class="col-md-6 text-center">
    {% include figure.liquid
       path="assets/projects/grad/rh3_kinematics/thumb_workspace.png"
       title="Thumb workspace"
       class="img-fluid rounded z-depth-1"
       width="100%" zoomable=true %}
    <div class="caption text-center">
      <strong>Thumb Workspace:</strong> Extensive 3D workspace produced by coupling T1, T2, and T3 palm rotations with continuum thumb bending.
    </div>
  </div>
</div>

---

## Simulation & Kapandji Opposability Test

The forward and inverse kinematics models were deployed in a **ROS and RViz** simulation environment to evaluate precision and manipulability:

- **Fingertip Trajectory Simulation:** Verified smooth, continuous fingertip paths corresponding to commanded airmass sequences.
- **Kapandji Opposability Test:** In clinical medicine, the Kapandji score evaluates thumb mobility by testing its ability to oppose and touch the tips of each long finger. Using the learned inverse kinematic models, the thumb successfully reached and touched the index, middle, ring, and little fingertips, confirming reachability and functional dexterity.

---

## Kinematics-Driven Fingertip Prediction App

Building upon the developed models, I designed and implemented a cross-platform **Flutter mobile application** for interactive control and visualization.

The app allows users to input target 3D Cartesian coordinates or pneumatic airmass values and receive real-time, bidirectional forward and inverse kinematics predictions with low computational overhead.

<div class="row justify-content-center">
  <div class="col-4 text-center">
    {% include video.liquid
       path="assets/projects/grad/rh3_kinematics/rh3_app_demo.mp4"
       class="img-fluid rounded z-depth-1"
       controls=true
       autoplay=false %}
    <div class="caption text-center">
      Flutter mobile app demo on Android: Real-time fingertip prediction and visualization.
    </div>
  </div>
</div>

---

## Technical Highlights

- **Robotic Platform:** RBO Hand 3 (compliant anthropomorphic soft robotic hand, TU Berlin)
- **Kinematic Paradigm:** Hybrid analytical DH parameter chains coupled with data-driven continuum neural models
- **Learning Models:** Shallow Feedforward MLPs (Dense) for finger compliance; $K$-NN regression ($k=12$, 76M points) for thumb IK
- **Tracking & Perception:** High-speed Motion Capture (MoCap) optical tracking of pneumatic inflation cycles
- **Simulation & Validation:** ROS Melodic · RViz · Clinical Kapandji Opposability Test
- **Software Stack:** Python · NumPy · TensorFlow · Flutter (Dart) for Android mobile app

---

## Team

**Sumit Patidar · Adrian Sieler (Mentor)**

---

## Technical Report

For complete Denavit-Hartenberg parameter tables, neural network hyperparameter specifications, MoCap marker placement schematics, and root-mean-square error (RMSE) tables, please refer to our full technical report:

- [**Download Project Report (PDF)**]({{ '/assets/projects/grad/rh3_kinematics/rh3_kinematics_technical_report.pdf' | relative_url }})
  - _Title:_ Learning Forward and Inverse Kinematics for Soft Pneumatic Actuators for Control and Visualization of the RBO Hand 3
  - _Author:_ Sumit Patidar
  - _Supervisor:_ Adrian Sieler
  - _Institution:_ Robotics and Biology Laboratory (RBO), Technical University of Berlin
