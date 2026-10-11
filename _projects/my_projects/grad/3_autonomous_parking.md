---
layout: page
title: Autonomous Navigation and Parking of a Robotic Car
description: Autonomous driving, dynamic mapping, and parking of a small-scale vehicle in MORSE simulation.
img: assets/projects/grad/autonomous_parking/perception.png
importance: 3
category: grad
related_publications: false
---

<div class="row justify-content-md-center">
    <div class="col-sm-10 text-center">
        {% include figure.liquid
            path="assets/projects/grad/autonomous_parking/semantic_map.png"
            title="Evaluation scene from MORSE simulation and RViz"
            width="100%"
            class="img-fluid rounded z-depth-1"
        %}
    </div>
</div>

<div class="caption text-center">
    Full autonomous driving evaluation: 3D MORSE simulation environment (top-left), real-time camera perception with sign detection (bottom-left), and RViz semantic map (right).
</div>

<div class="text-center my-3">
    <a href="{{ '/assets/projects/grad/autonomous_parking/autonomous_parking_technical_report.pdf' | relative_url }}" target="_blank" rel="noopener noreferrer" class="btn btn-outline-primary btn-sm">
        <i class="fa-solid fa-file-pdf"></i> Read Technical Report (PDF)
    </a>
</div>

## Overview

Self-driving vehicles require robust integration across sensing, perception, dynamic world modeling, motion planning, and decision making to safely navigate urban environments.

Completed at the **Distributed Artificial Intelligence Laboratory (DAI-LABOR)**, Technical University of Berlin (TU Berlin), as part of the _Applications of Robotics and Autonomous Systems_ project, this work developed an autonomous driving stack for a small-scale 4WD robotic car simulated in the MORSE (Modular Open Robots Simulation Engine) environment on ROS.

The objective was to enable the vehicle to follow lane markings, recognize and obey traffic signs, avoid static and moving obstacles (pedestrians and vehicles), manage battery status, and execute an autonomous parking maneuver into an identified parking spot.

---

## My Contributions

- **Perception System Integration:** Performed system integration of YOLO models into the ROS software pipeline for real-time detection of traffic signs and obstacles.
- **Costmap Layer Integration:** Combined different static layers (road lane boundaries, static obstacles, and inflation) into a unified 2D costmap for safe vehicle navigation and motion planning.
- **Local Planning & Trajectory Generation:** Configured and tuned the Timed Elastic Band (`teb_local_planner`) local motion planner to produce smooth, collision-free velocity commands (`/cmd_vel`) respecting the vehicle's non-holonomic kinematic constraints.
- **Decision Making & Behavior Management:** Developed a finite state machine (FSM) behavior coordinator managing vehicle state transitions between idle, lane driving, emergency braking, battery recharging, and parking.

---

## System

The autonomous system follows an integrated modular pipeline:

**Sensors (LiDAR, Camera, IMU, Odometry) $\to$ Perception & State Estimation $\to$ Dynamic Costmap Layering $\to$ Global & Local Path Planning $\to$ FSM Behavior Execution $\to$ Actuation (`/cmd_vel`)**

### 1. Software Architecture

The software architecture is structured into four functional tiers:

<div class="row justify-content-md-center mb-3">
    <div class="col-sm-12 text-center">
        {% include figure.liquid
            path="assets/projects/grad/autonomous_parking/sys_arch.png"
            title="ROS System Architecture"
            width="100%"
            class="img-fluid rounded z-depth-1"
            zoomable=true
        %}
        <div class="caption">Four-tier ROS architecture: Sensor-Motor level (MORSE), Low-level Sensing & Motion Planners, High-level Navigation Planners, and Application Meta-level.</div>
    </div>
</div>

- **Sensor-Motor Level (MORSE):** Publishes raw LiDAR scans, forward and rear camera RGB feeds, wheel odometry, IMU data, and battery status.
- **Sensing & Low-Level Planners:** Fuses laser odometry (`rf2o_laser_odometry`), wheel encoders, and IMU via an Extended Kalman Filter (`ekf_se`), computes SLAM maps (`hector_mapping`), and updates multi-layered costmaps.
- **High-Level Navigation & Perception:** Runs YOLO object and sign detection, generates 2D lane boundaries, computes global routes with A*, and executes the TEB local planner.
- **Application Level:** Governs task execution, battery monitoring, and parking spot selection.

### 2. Perception & Multi-Layer Dynamic Mapping

The vehicle perceives its surroundings using front/rear cameras and 2D LiDAR. To provide the motion planner with an actionable representation of the world, sensor outputs are fused into a multi-layered Local Dynamic Map (LDM):

<div class="row justify-content-center align-items-center mb-3">
    <div class="col-md-6 text-center mb-3 mb-md-0">
        {% include figure.liquid
            path="assets/projects/grad/autonomous_parking/perception.png"
            title="YOLO traffic sign and obstacle detection"
            width="100%"
            class="img-fluid rounded z-depth-1"
            zoomable=true
        %}
        <div class="caption"><strong>Perception:</strong> Real-time YOLO detection of traffic signs (construction, directional arrows) and track boundaries.</div>
    </div>
    <div class="col-md-6 text-center">
        {% include figure.liquid
            path="assets/projects/grad/autonomous_parking/dynamic_map.png"
            title="Multi-layer Costmap Architecture"
            width="100%"
            class="img-fluid rounded z-depth-1"
            zoomable=true
        %}
        <div class="caption"><strong>Local Dynamic Map:</strong> Layered costgrid combining roadlanes, moving obstacles, obstacle bounds, inflation, and static geometry.</div>
    </div>
</div>

### 3. Lane Mapping & Behavior Decision Making

Navigation relies on road lane mapping combined with high-level behavioral control:

<div class="row justify-content-center align-items-center mb-3">
    <div class="col-md-6 text-center mb-3 mb-md-0">
        {% include figure.liquid
            path="assets/projects/grad/autonomous_parking/lane.png"
            title="2D lane detection and mapping"
            width="100%"
            class="img-fluid rounded z-depth-1"
            zoomable=true
        %}
        <div class="caption"><strong>2D Lane Mapping:</strong> Occupancy grid representation of track layout and drivable corridor boundaries.</div>
    </div>
    <div class="col-md-6 text-center">
        {% include figure.liquid
            path="assets/projects/grad/autonomous_parking/decision_making.JPG"
            title="Finite State Machine Decision Making"
            width="100%"
            class="img-fluid rounded z-depth-1"
            zoomable=true
        %}
        <div class="caption"><strong>Behavior Executive:</strong> Finite State Machine arbitrating between IDLE, DRIVING, RECHARGING, and PARKING states.</div>
    </div>
</div>

---

## Results & Key Capabilities

- **Lane Keeping & Navigation:** The vehicle successfully maintained lane boundaries along continuous curved tracks using the fused 2D lane costmap and global A* route.
- **Traffic Sign Compliance:** Real-time sign detection triggered appropriate driving behaviors, including decelerating through construction zones and respecting directional turning commands at intersections.
- **Dynamic Obstacle Avoidance:** Moving pedestrians and other vehicles were tracked, predicted, and reflected on the dynamic costmap layer, triggering reactive braking and safe re-routing.
- **Autonomous Parking Execution:** Upon receiving a parking goal, the vehicle transitioned from road-following to local trajectory generation, reversing and aligning into the designated parking bay without collision.

---

## Technical Highlights

- **Simulation Platform:** MORSE (Modular Open Robots Simulation Engine) · Blender · ROS Melodic · Ubuntu 18.04
- **Perception Pipeline:** YOLOv3 / SSD deep learning detection · Camera RGB-D streams · 2D LiDAR scanning
- **State Estimation & SLAM:** Extended Kalman Filter (`robot_localization` / `ekf_se`) · `hector_mapping` · `rf2o_laser_odometry`
- **Costmap Architecture:** Multi-layered 2D Costmap (Static, Road Lane, Obstacle, Inflation, and Moving Entities)
- **Path & Motion Planning:** Global A* Planner · Timed Elastic Band (`teb_local_planner`) with non-holonomic vehicle kinematics
- **Behavior Executive:** Finite State Machine (FSM) & Behavior Trees managing driving, charging, and parking logic
- **Control Interface:** Twist force actuator command generation (`/cmd_vel`) with linear and steering PID control

---

## Team

**Alexandros Nikolaou · Sharang Kaul · Sumit Patidar · Jhorman Perez · Stoyan Karastoyanov · Janis Freund**

---

## Technical Report

For the complete system design specifications, sensor calibration parameters, ROS topic message definitions, and detailed node interfaces, please refer to our full project report:

- [**Download Project Report (PDF)**]({{ '/assets/projects/grad/autonomous_parking/autonomous_parking_technical_report.pdf' | relative_url }})
  - _Title:_ Prediction, Perception and Advanced AD Capabilities: System Design Specifications
  - _Authors:_ Alexandros Nikolaou, Sharang Kaul, Sumit Patidar, Jhorman Perez, Stoyan Karastoyanov, Janis Freund
  - _Institution:_ Distributed Artificial Intelligence Laboratory (DAI-LABOR), Technical University of Berlin (TUB, March 2021)
