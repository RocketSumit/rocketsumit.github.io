---
layout: page
title: Soft Hand Kinematics
description: Learning Kinematics of a Soft Hand
img: assets/projects/rh3/rh3.gif
importance: 1
category: grad
---

## About

The RBO hand 3 is a soft robotic hand developed at Robotics and Biology
Laboratory (RBO) at Technical University of Berlin. It is a highly compliant
hand designed for dexterous grasping. The inherent compliance of the fingers
makes it hard to model them analytically unlike their rigid links counterparts.
Therefore, in this project, we investigate efficient data-driven approach to
learn the forward and inverse kinematic models of the hand to control and
visualize the hand in free space.

We used a small feed-forward network to model the pose of fingertips as a
function of airmass. In addition, palm and T{1-3} bellow actuators are modeled
as revolut joints. The ring and little finger, and thumb form a chain of
connected joints with their respective bellows. The final finger pose is
computed by taking into account airmass in each finger compartments along with
palm and thumb bellows (T1,T2,T3).

<div class="row justify-content-md-center">
    <div class="col-sm-6">
    {% include
    figure.liquid path="assets/projects/rh3/rh3_components.png" title="rh3
    hand" width="100%" class="img-fluid rounded z-depth-1" %}
        <div class="caption"> The RBO Hand 3. Each finger has two pressure
    chambers except thumb which has one chamber. </div>
    </div>
    <div class="col-sm-6"> {% include figure.liquid
        path="assets/projects/rh3/all_finger_heatmap.png" title="rh3
        workspace" width="100%" class="img-fluid rounded z-depth-1" %}
        <div class="caption"> Reachable workspace of the finger
    tips (without palm bellow and T1, T2, T3 bellow actuation) </div>
    </div>
    <div class="col-sm-6"> {% include figure.liquid
        path="assets/projects/rh3/ring_little_combined_workspace.png"
        title="rh3 workspace" width="100%" class="img-fluid rounded z-depth-1"
        %}
        <div class="caption"> Reachable
    workspace of the little and ring finger with palm actuation </div>
    </div>
    <div class="col-sm-6"> {% include figure.liquid
        path="assets/projects/rh3/thumb_workspace.png" title="rh3
        workspace" width="100%" class="img-fluid rounded z-depth-1" %}
        <div class="caption"> Reachable
    workspace of the thumb with T1, T2 and T3 bellow actuations </div>
    </div>
</div>

## Team

Sumit Patidar, Adrian Sieler (Mentor)

## References

[1] [Puhlmann, S., Harris, J. and Brock, O., 2022. RBO hand 3: A platform for soft dexterous manipulation. IEEE Transactions on Robotics, 38(6), pp.3434-3449.](https://ieeexplore.ieee.org/abstract/document/9761831/)

[2] [Bhatt, A., Sieler, A., Puhlmann, S. and Brock, O., 2022. Surprisingly robust in-hand manipulation: An empirical study. arXiv preprint arXiv:2201.11503.](https://arxiv.org/abs/2201.11503)
