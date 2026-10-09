---
layout: page
title: Numerical vs Neural Network based Kinematics Solver
description: Investigating numerical and deep neural network-based inverse kinematics solvers for a 7-DOF redundant manipulator.
img: assets/projects/grad/traditional_vs_nn_solver/circle_kuka.png
importance: 4
category: grad
related_publications: false
---

<div class="row justify-content-md-center">
    <div class="col-sm-4 text-center">
        {% include figure.liquid
            path="assets/projects/grad/traditional_vs_nn_solver/circle_kuka.png"
            title="KUKA LBR iiwa circular trajectory in Gazebo"
            width="100%"
            class="img-fluid rounded z-depth-1"
        %}
    </div>
</div>

<div class="caption text-center">
    Simulation of the 7-DOF KUKA LBR iiwa executing a spatial circular trajectory in ROS & Gazebo.
</div>

<div class="text-center my-3">
    <a href="{{ '/assets/projects/grad/traditional_vs_nn_solver/nn_kinematics_technical_report.pdf' | relative_url }}" target="_blank" rel="noopener noreferrer" class="btn btn-outline-primary btn-sm">
        <i class="fa-solid fa-file-pdf"></i> Read Technical Report (PDF)
    </a>
</div>

## Overview

Finding inverse kinematics (IK) solutions for redundant manipulators is a fundamental challenge in robotics. For a 7-degree-of-freedom (7-DOF) manipulator like the **KUKA LBR iiwa**, closed-form analytical solutions do not generally exist due to kinematic redundancy and non-linear geometric constraints.

Traditional iterative numerical methods (such as Jacobian-based solvers) are widely used across the industry. However, they can require substantial computational power per step, suffer from kinematic singularities, or exhibit slow convergence in real-time control loops. Artificial Neural Networks (ANNs) offer an alternative data-driven approach that can predict joint configurations with constant-time inference and GPU parallelization.

Completed as part of a graduate research project for course **II2202 at KTH Royal Institute of Technology**, this computational study benchmarks popular iterative numerical solvers (Jacobian Transpose, Pseudo-Inverse, and SVD) against multi-layer perceptron (Dense) and Convolutional Neural Network (CNN) architectures. We evaluated convergence rate, execution time, and trajectory tracking fidelity across linear, square, and circular Cartesian trajectories.

---

## My Contributions

- **Kinematic Solvers & Implementation:** Formulated and implemented iterative Jacobian-based algorithms (Jacobian Transpose, Moore-Penrose Pseudo-Inverse, and Singular Value Decomposition) in Python.
- **Simulation Pipeline:** Built the simulation environment integrating ROS Melodic and Gazebo 9 to benchmark the 7-DOF KUKA LBR iiwa on 3D spatial trajectories under error tolerances ranging from $10^{-1}\,\text{m}$ to $10^{-6}\,\text{m}$.
- **Dataset Synthesis:** Synthesized a 5-million sample forward kinematics dataset mapping end-effector Cartesian poses (6D) to joint angles (7D), applying deduplication and normalization.
- **Custom Loss Formulation:** Formulated the forward-kinematics-aware custom loss function, evaluating position and orientation errors directly in task space to address the many-to-one ambiguity of redundant manipulators.
- **Empirical Benchmarking:** Evaluated accuracy, iteration counts, and inference latency between traditional numerical solvers and neural network models.

---

## System

The evaluation framework follows an end-to-end simulation and benchmarking workflow:

**Target Trajectory $\to$ IK Solver (Iterative / ANN) $\to$ Joint Angle Commands $\to$ Gazebo Physics Simulation $\to$ Trajectory Tracking Analysis**

### 1. Kinematics Approaches Compared

We compared three primary paradigms to solve inverse kinematics:

<div class="row justify-content-center align-items-center mb-3">
    <!-- Column 1: Direct Mappings (Analytical & Data-Driven) -->
    <div class="col-md-8 text-center mb-3 mb-md-0">
        <div class="mb-3">
            {% include figure.liquid
                path="assets/projects/grad/traditional_vs_nn_solver/analytical.svg"
                title="Analytical kinematics formulation"
                width="100%"
                class="img-fluid rounded z-depth-1"
                zoomable=true
            %}
            <div class="caption"><strong>Analytical IK:</strong> Closed-form, but unfeasible for redundant 7-DOF arms.</div>
        </div>
        <div>
            {% include figure.liquid
                path="assets/projects/grad/traditional_vs_nn_solver/nn_kinematics.svg"
                title="Neural network kinematics"
                width="100%"
                class="img-fluid rounded z-depth-1"
                zoomable=true
            %}
            <div class="caption"><strong>Data-Driven IK:</strong> Direct non-linear mapping from 6D pose to 7D joint angles.</div>
        </div>
    </div>

    <!-- Column 2: Iterative Optimization Loop -->
    <div class="col-md-4 text-center">
        {% include figure.liquid
            path="assets/projects/grad/traditional_vs_nn_solver/numerical_optimization.svg"
            title="Iterative numerical optimization"
            width="100%"
            class="img-fluid rounded z-depth-1"
            zoomable=true
        %}
        <div class="caption"><strong>Iterative IK:</strong> Solves $\Delta \Theta = J^\dagger \Delta X$ iteratively until convergence.</div>
    </div>

</div>

### 2. Network Architectures & Custom Loss

Because inverse kinematics for redundant arms is a many-to-one mapping, training with standard Mean Squared Error (MSE) in joint space often causes conflicting gradients when multiple valid joint configurations reach the same end-effector pose.

To address this, we formulated a **custom forward-kinematics loss function** that evaluates error directly in task space:

<div class="row justify-content-md-center mb-3">
    <div class="col-md-8 text-center">
        {% include figure.liquid
            path="assets/projects/grad/traditional_vs_nn_solver/custom_loss.jpeg"
            title="Custom loss function"
            width="100%"
            class="img-fluid rounded z-depth-1"
            zoomable=true
        %}
        <div class="caption">Custom loss: Penalizes task-space position error and orientation cross-product error via forward kinematics.</div>
    </div>
</div>

We evaluated both fully connected (Dense) and 1D/2D Convolutional Neural Network (CNN) architectures to learn the non-linear mappings:

<div class="row justify-content-md-center mb-3">
    <div class="col-md-6 text-center mb-3 mb-md-0">
        {% include figure.liquid
            path="assets/projects/grad/traditional_vs_nn_solver/dense.png"
            title="Dense neural network architecture"
            width="100%"
            class="img-fluid rounded z-depth-1"
            zoomable=true
        %}
        <div class="caption">Dense architecture: Fully connected layers mapping 6D pose to 7D joint configuration.</div>
    </div>
    <div class="col-md-6 text-center">
        {% include figure.liquid
            path="assets/projects/grad/traditional_vs_nn_solver/cnn.png"
            title="CNN neural network architecture"
            width="100%"
            class="img-fluid rounded z-depth-1"
            zoomable=true
        %}
        <div class="caption">CNN architecture: Exploits spatial representations to improve generalization.</div>
    </div>
</div>

---

## Results & Key Findings

We evaluated trajectory tracking across three test profiles (linear, square, and circular) using both numerical methods and trained networks.

<div class="row justify-content-md-center">
    <div class="col-md-4 text-center mb-3">
        {% include figure.liquid
            path="assets/projects/grad/traditional_vs_nn_solver/circle_transpose.png"
            title="Jacobian Transpose trajectory"
            width="100%"
            class="img-fluid rounded z-depth-1"
            zoomable=true
        %}
        <div class="caption"><strong>Jacobian Transpose:</strong> Slower convergence and noticeable trajectory deviation under strict tolerances.</div>
    </div>
    <div class="col-md-4 text-center mb-3">
        {% include figure.liquid
            path="assets/projects/grad/traditional_vs_nn_solver/circle_pseudo.png"
            title="Jacobian Pseudo-inverse trajectory"
            width="100%"
            class="img-fluid rounded z-depth-1"
            zoomable=true
        %}
        <div class="caption"><strong>Jacobian Pseudo-Inverse:</strong> Highly accurate tracking, consistently converging within ~2 iterations.</div>
    </div>
    <div class="col-md-4 text-center mb-3">
        {% include figure.liquid
            path="assets/projects/grad/traditional_vs_nn_solver/circle_nn.png"
            title="CNN trajectory"
            width="100%"
            class="img-fluid rounded z-depth-1"
            zoomable=true
        %}
        <div class="caption"><strong>Proposed CNN:</strong> Smooth circular profile with fast ~15 ms GPU inference, but with minor sub-millimeter offset.</div>
    </div>
</div>

### Key Takeaways

1. **Jacobian SVD & Pseudo-Inverse vs. Transpose:** Jacobian SVD and Pseudo-Inverse converged identically well in ~2 iterations ($<10\,\text{ms}$) down to high precision ($10^{-6}\,\text{m}$). In contrast, Jacobian Transpose required 80 to 370+ iterations, degrading rapidly as the error tolerance tightened.
2. **Custom Loss vs. Standard MSE:** Networks trained with the task-space custom loss function converged faster and yielded significantly lower tracking error than models trained with standard joint-space MSE.
3. **CNN vs. Dense Generalization:** While the dense network achieved lower loss on the training set, the CNN architecture generalized noticeably better on unseen trajectories due to reduced overfitting.
4. **Execution Time vs. Precision:** The trained neural network computed the entire circular trajectory in $\approx 15\,\text{ms}$ on GPU. While it fell short of the sub-millimeter precision of iterative solvers, its rapid execution makes it well-suited for fast initial approximations or real-time reactive seeding.

---

## Technical Highlights

- **Manipulator:** 7-DOF KUKA LBR iiwa robotic arm
- **Simulation:** ROS Melodic · Gazebo 9.0 · Ubuntu 18.04
- **Numerical Solvers:** Jacobian Transpose, Moore-Penrose Pseudo-Inverse ($J^\dagger = J^T(JJ^T)^{-1}$), and SVD
- **Learning Stack:** TensorFlow 1.15 · TensorFlow Graphics · Docker GPU environment
- **Architectures:** Multi-Layer Perceptron (Dense) and Convolutional Neural Network (CNN)
- **Dataset:** 5 million forward kinematics mappings (6D pose $\leftrightarrow$ 7D joint space) with deduplication
- **Loss Formulation:** Forward-kinematics task-space loss penalizing Euclidean position and rotational error
- **Benchmarked Trajectories:** 3D Linear, Square, and Circular paths
- **Key Metrics:** Constant ~2 iterations for Jacobian Pseudo-Inverse; ~15 ms full-trajectory GPU inference for CNN

---

## Team

**Sumit Patidar · Utkarsh Kunwar**

---

## Technical Report

For the complete mathematical formulations, hyperparameter tables, loss convergence plots, and detailed multi-trajectory benchmarks, please refer to our full technical report:

- [**Download Project Report (PDF)**]({{ '/assets/projects/grad/traditional_vs_nn_solver/nn_kinematics_technical_report.pdf' | relative_url }})
  - _Title:_ Popular Traditional and Neural Network-Based Methods for Solving Inverse Kinematics of Complex Manipulators: A Computational Study
  - _Authors:_ Sumit Patidar & Utkarsh Kunwar
  - _Institution:_ KTH Royal Institute of Technology, Stockholm, Sweden (Course II2202)
