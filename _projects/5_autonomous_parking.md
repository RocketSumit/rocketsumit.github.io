---
layout: page
title: Autonomous Navigation and Parking of a Robotic Car
description: Simulating a robotic car in Morse simulator
img: assets/img/projects/autonomous_driving/perception.png
importance: 2
category: grad
---

## About

The main objective of this project is to drive the robotic car autonomously and
park in the identified parking spot in the simulation environment while
following the constraints. The main contribution lies in detecting
static, dynamic objects and road lanes and creating a dynamic map based on
projections for motion planning. The project work includes implementing
an online prediction module using a RNN, tuning a Time Elastic Band (TEB) local
planner, and implementing a finite state machine-based decision-maker to park
the car autonomously.

## Architecture

<div class="row justify-content-md-center">
    <div class="col-sm-12">
        {% include
    figure.liquid path="assets/img/projects/autonomous_driving/sys_arch.png"
    title="system architecture" width="100%" class="img-fluid rounded
    z-depth-1" %}
    </div>
    <div class="caption col-sm-12"> Software architecture </div>
</div>

## Results

<div class="row justify-content-md-center">
    <div class="col-sm-6">
        {% include figure.liquid
        path="assets/img/projects/autonomous_driving/dynamic_map.png"
        title="dynamic costmap" width="100%" class="img-fluid rounded
        z-depth-1" %}
    </div>
    <div class="col-sm-6"> {% include figure.liquid
        path="assets/img/projects/autonomous_driving/lane.png" title="lane
        costmap" width="100%" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="caption col-sm-6"> Costmap layers </div>
    <div class="caption col-sm-6"> 2D lane mapping  </div>

</div>
<div class="row justify-content-md-center">
    <div class="col-sm-7">
    {% include figure.liquid
        path="assets/img/projects/autonomous_driving/semantic_map.png"
        title="semantic map" width="100%" class="img-fluid rounded z-depth-1"
        %}
    </div>
    <div class="col-sm-5">
        {% include figure.liquid
        path="assets/img/projects/autonomous_driving/decision_making.JPG"
        title="decision making" width="100%" class="img-fluid rounded
        z-depth-1" %}
    </div>
    <div class="caption col-sm-7"> Evalution scene from the Morse environment </div>
    <div class="caption col-sm-5"> Decision making using finite-state machine </div>
</div>

## Team

Sumit Patidar, Alexandros Nikolaou, Sharang Kaul, Janis Freund, Jhorman Perez,
Stoyan Karastoyanov