---
layout: page
title: Numerical vs Neural Network based Kinematics Solver
description: Investigating different inverse kinematics solver for complex manipulators
img: assets/img/projects/nnkinematics_7dof/circle_kuka.png
importance: 1
category: grad
---

## About

Inverse kinematics solutions for complex systems are difficult to find and
closed-form analytical solutions may not always exist. Resorting to iterative
numerical methods requires heavy computation and affect performance in
real-time applications. Numerical solutions sometimes also suffer from
singularities which can lead to a misbehaving system while other solutions
might have too slow a convergence. Iterative algorithms are used widely and
solutions using artificial neural networks have also been introduced in recent
years. Therefore, this project investigates the performances of solutions to
the inverse kinematics problem using different popular iterative methods and
neural networks. The performance of different architectures and the effect of
hyper-parameters were compared against the Jacobian based iterative methods.

## Proposed Network Architectures

<div class="row justify-content-md-center">
    <div class="col-sm-6">
        {% include
    figure.liquid path="assets/img/projects/nnkinematics_7dof/dense.png"
    title="system architecture" width="100%" class="img-fluid rounded
    z-depth-1" %}
    </div>
    <div class="col-sm-6">
        {% include
    figure.liquid path="assets/img/projects/nnkinematics_7dof/cnn.png"
    title="system architecture" width="100%" class="img-fluid rounded
    z-depth-1" %}
    </div>
</div>
<div class="row justify-content-md-center">
<div class="caption col-sm-6"> Dense architecture for 7DOF arm </div>
<div class="caption col-sm-6"> CNN architecture for 7DOF arm </div>
</div>

## Results

Among the Jacobian methods, it was observed that for trivial trajectories, the
Jacobian inverse-based solutions converged faster and were far more accurate
than the Jacobian transpose-based method. For the inverse kinematic solution
using neural network, it was observed that the proposed network architecture
and custom loss function performed better than the state-of-the-art networks
with standard mean-squared error for the case of 7 degree of freedom robotic
manipulator. Compared to the iterative methods, the solution proposed by the
network fell short in accuracy but performed on par in terms of execution time.

<div class="row justify-content-md-center">
    <div class="col-sm-4">
        {% include
    figure.liquid path="assets/img/projects/nnkinematics_7dof/circle_kuka.png"
    title="system architecture" width="100%" class="img-fluid rounded
    z-depth-1" %}
    </div>
    <div class="col-sm-6">
        {% include
    figure.liquid path="assets/img/projects/nnkinematics_7dof/circle_transpose.png"
    title="system architecture" width="100%" class="img-fluid rounded
    z-depth-1" %}
    </div>
    <div class="caption col-sm-4"> Simulation of Circular trajectory in Gazebo </div>
    <div class="caption col-sm-6"> Trajectory using Jacobian Transpose </div>
    <div class="col-sm-6">
        {% include
    figure.liquid path="assets/img/projects/nnkinematics_7dof/circle_pseudo.png"
    title="system architecture" width="100%" class="img-fluid rounded
    z-depth-1" %}
    </div>
    <div class="col-sm-6">
        {% include
    figure.liquid path="assets/img/projects/nnkinematics_7dof/circle_nn.png"
    title="system architecture" width="100%" class="img-fluid rounded
    z-depth-1" %}
    </div>
    <div class="caption col-sm-6"> Trajectory using Jacobian Pseudo-inverse </div>
    <div class="caption col-sm-6"> Trajectory using CNN (better than dense)</div>
</div>

## Team

Sumit Patidar, Utkarsh Kunwar
