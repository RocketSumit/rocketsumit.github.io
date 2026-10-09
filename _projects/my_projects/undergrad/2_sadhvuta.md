---
layout: page
title: Sadhvuta
description: A mobile trash sorting robot.
img: assets/projects/undergrad/sadhvuta/logo.jpg
importance: 2
category: undergrad
---

<div class="row justify-content-sm-center">
    <div class="col-sm">
{% include figure.liquid path="assets/projects/undergrad/sadhvuta/front.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm">
{% include figure.liquid path="assets/projects/undergrad/sadhvuta/side1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm">
{% include figure.liquid path="assets/projects/undergrad/sadhvuta/side2.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>

<div class="caption"> Sadhvuta — Robot Prototype </div>

## Overview

**Sadhvuta** is a four-wheeled, battery-powered mobile trash-sorting robot designed
to automate waste segregation and reduce littering around campus.

The robot can be remotely driven to a waste collection point, where users
deposit trash one item at a time. Each item is automatically classified into
**paper, metal, or plastic** using a CNN-based vision system with **97%
classification accuracy**. Based on the predicted category, a mechanical
sorting mechanism routes the waste into the corresponding collection bin.

The project combines **mobile robotics, computer vision, mechatronics, and
automated waste handling** into a single physical system.

---

## My Contributions

- **Mechatronics:** Designed and integrated the mechanical and electromechanical components responsible for waste handling and sorting.
- **System Integration:** Integrated the mobility, sensing, classification, and mechanical sorting subsystems into a functional end-to-end prototype.
- **Team Management:** Coordinated technical tasks and project execution across the team, ensuring integration between mechanical, electrical, and software components.

---

## System

The system operates as a pipeline:

**Remote Navigation → Waste Detection → CNN Classification → Category Selection → Mechanical Sorting → Dedicated Waste Bin**

Once the robot reaches a collection point, the user inserts a single waste
item. The vision system classifies the item into one of three categories —
**paper, metal, or plastic** — and the sorting mechanism automatically directs it
to the corresponding bin.

---

## Technical Highlights

- **Platform:** Four-wheeled, battery-powered mobile robot
- **Mobility:** Remote-controlled drive system
- **Classification:** CNN-based waste classification
- **Classification Accuracy:** 97%
- **Waste Categories:** Paper, metal, plastic
- **Sorting:** Automated mechanical waste segregation
- **Mechatronics:** Mechanical sorting mechanism + electromechanical integration
- **System Integration:** Mobility, perception, classification, and sorting subsystems
- **Application:** Automated waste collection and segregation

---

## Team

**Sumit Patidar · Dhruv Patel · Versha Dhankar · Vishawajeet Patel · Aditya Sharma · Aksh Gautam**
