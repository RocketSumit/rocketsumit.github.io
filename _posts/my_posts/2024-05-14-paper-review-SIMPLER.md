---
layout: post
title: Paper Review - SIMPLER
date: 2024-05-14 20:00:00 # TODO: update
description:
tags: paper-reviews
categories: robotics
related_posts: false
toc:
  beginning: true
---

# [Evaluating Real-World Robot Manipulation Policies in Simulation](https://simpler-env.github.io)

**Xuanlin Li**<sup>\*</sup><sup>1</sup>, **Kyle Hsu**<sup>\*</sup><sup>2</sup>, **Jiayuan Gu**<sup>\*</sup><sup>1</sup>, **Karl Pertsch**<sup>†</sup><sup>2,3</sup>, **Oier Mees**<sup>†</sup><sup>3</sup>, **Homer Rich Walke**<sup>3</sup>, **Chuyuan Fu**<sup>4</sup>, **Ishikaa Lunawat**<sup>2</sup>, **Isabel Sieh**<sup>2</sup>, **Sean Kirmani**<sup>4</sup>, **Sergey Levine**<sup>3</sup>, **Jiajun Wu**<sup>2</sup>, **Chelsea Finn**<sup>2</sup>, **Hao Su**<sup>‡</sup><sup>1</sup>, **Quan Vuong**<sup>‡</sup><sup>4</sup>, **Ted Xiao**<sup>‡</sup><sup>4</sup>

<sup>\*</sup>Equal contribution
<sup>†</sup>Core contributors
<sup>‡</sup>Equal advising

<sup>1</sup>UC San Diego, <sup>2</sup>Stanford University, <sup>3</sup>UC Berkeley, <sup>4</sup>Google DeepMind

## 1. How should we evaluate policies trained on real robot data?

<div class="row justify-content-md-center">
  <div class="col-sm-10 text-center">
      {% include figure.liquid path="assets/paper-reviews/simpler/1.png" width="75%" class="img-fluid rounded z-depth-1" %}
      <div class="caption text-center"> Train on real, evaluate in real </div>
    </div>
</div>

Generally, roboticist evaluate policies (trained on realworld) in realworld. However, there are some problems associated with it.

- People bump into cameras
- Gripper gets stuck
- Real-world evaluation is slow and tedious
- Difficult to reproduce experiments

## 2. Potential SIMPLER way

SIMPLER stands for **SIMULATED MANIPULATION POLICY EVALUATION FOR REAL ROBOT SETUPS**

<div class="row justify-content-md-center">
  <div class="col-sm-10 text-center">
    {% include figure.liquid path="assets/paper-reviews/simpler/2.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> Train on real, evaluate in real </div>
  </div>
</div>

## 3. How real and SIMPLER performance correlates?

<div class="row justify-content-md-center">
  <div class="col-sm-5 text-center">
    {% include figure.liquid path="assets/paper-reviews/simpler/correlation.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> Real and sim performance correlation </div>
  </div>
</div>

## 4. Problem definition

- NOT to obtain 1:1 reproduction of policies' real-world behavior
- To guide policy improvement decisions
- Construct a simulator S with a strong correlation between relative performances in real and sim

## 5. Metrics

The paper propose two metrics to measure the performance in sim vs real:

- Pearson correlation coefficient (Pearson r)
- Mean Maximum Rank Violation (MMRV)

<div class="row justify-content-md-center">
  <div class="col-sm-6 text-center">
    {% include figure.liquid path="assets/paper-reviews/simpler/pearson_coefficient.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> Pearson correlation coefficient (r) </div>
  </div>
  <div class="col-sm-6 text-center">
    {% include figure.liquid path="assets/paper-reviews/simpler/mean_maximum_rank_violation.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> Mean Maximum Rank Violation to overcome some limitation of Pearson correlation coefficient (r) </div>
  </div>
</div>

## 6. Challenges to building a real-to-sim evaluation system

**6.1 Mitigating the Real-to-Sim Control Gap - SysID (System Identification)**

- Optimize P,D values for sim controller (stiffness, damping factors)
- Play a demo trajectory actions on both sim and real

<div class="row justify-content-md-center">
  <div class="col-sm-6 text-center">
    {% include figure.liquid path="assets/paper-reviews/simpler/sysid.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> Minimizing the loss function to mitigate the control gap. </div>
  </div>
</div>

**6.2 Mitigating the Real-to-Sim Visual Gap**

The goal is to match the simulator visuals to those of the real-world environment with only a modest amount of manual effort using **Green screening and Texture matching**.

<div class="row justify-content-md-center">
  <div class="col-sm-8 text-center">
    {% include figure.liquid path="assets/paper-reviews/simpler/visual_gap.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> Replacing simulation background with real-world background and object textures with real-world textures. </div>
  </div>
</div>

## 7. Simulation setup

Two manipulation setups are used for different tasks.

<div class="row justify-content-md-center">
  <div class="col-sm-10 text-center">
    {% include figure.liquid path="assets/paper-reviews/simpler/simulation_setup.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> Simulation setup 1) Using Google Robot 2) Using WidowX robot (BrideData V2 dataset) </div>
  </div>
</div>

## 8. Investigations for simulation evaluations

The paper investigates the following key questions:

- Relative performances in sim and real
- Sensitivity to various visual distribution shifts
- Sensitivity to control and visual gaps
- Sensitivity to physical property gaps
- Does results extend to different physics simulator?

## 9. Experiment setup

They evaluate different open-source robot policies on the simulation setup described above. For google robot, four versions of robot arm and gripper colors used.

- RT-1 (Begin)
- RT-1 (15%)
- RT-1 (Converged)
- RT-1-X
- RT-2-X
- Octo-Base
- Octo-Small

## 10. Results

SIMPLER can be used to evaluate diverse sets of rigid-body tasks (non-articulated / articulated objects, tabletop / non-tabletop tasks, shorter / longer horizon tasks), with many intra-task variations (e.g., different object combinations; different object / robot positions and orientations), for each of two robot embodiments (Google Robot and WidowX).

**10.1 Evaluating and comparing policies**

<div class="row justify-content-md-center">
  <div class="col-sm-12 text-center">
    {% include figure.liquid path="assets/paper-reviews/simpler/results_google_and_widow_robot.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> Policy performances evaluated in SIMPLER have strong correlation with those in the real world (illustrated by low MMRV and high Pearson r). </div>
  </div>
</div>

**10.2 Analyzing and predicting policy behaviors under distribution shifts**

<div class="row justify-content-md-center">
  <div class="col-sm-12 text-center">
    {% include figure.liquid path="assets/paper-reviews/simpler/results_distribution_shifts.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> SIMPLER can be used to analyze the policies' finegrained behaviors, such as their robustness to common distribution shifts like lightings, backgrounds, camera poses, distractor objects, and table textures. </div>
  </div>
</div>

## 11. Ablations

<div class="row justify-content-md-center">
  <div class="col-sm-6 text-center">
    {% include figure.liquid path="assets/paper-reviews/simpler/ablation_effects_of_sysid.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> Control loss is proportional to the Mean Maximum Rank Violation. </div>
  </div>
  <div class="col-sm-6 text-center">
    {% include figure.liquid path="assets/paper-reviews/simpler/ablations_effects_of_visual_matching.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> Real-Sim Success Gap is miminum when all visual aspects of experiments match. </div>
  </div>
  <div class="col-sm-6 text-center">
    {% include figure.liquid path="assets/paper-reviews/simpler/ablation_physical_properties.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> If physical properties of the objects are varied, the correlation still remains intact, have <= 15% impact on success rates. </div>
  </div>
  <div class="col-sm-6 text-center">
    {% include figure.liquid path="assets/paper-reviews/simpler/ablation_simulation.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption"> The Real-Sim performance correlation is invariant to the simulator. </div>
  </div>
</div>

## 12. Conclusion

- SIMPLER seems good proxy for real world policy evaluations
- Limitations
  - No manipulation tasks with soft-objects
  - No tasks with high motion dynamics
  - Green screening
    - Fixed cameras
    - No shadows and visual details
  - Manual effort in creating simulation evaluation environments is still high

## 13. BibTex

To cite this paper:

```
 @article{li24simpler,
        title={Evaluating Real-World Robot Manipulation Policies in Simulation},
        author={Xuanlin Li and Kyle Hsu and Jiayuan Gu and Karl Pertsch and Oier Mees and Homer Rich Walke and Chuyuan Fu and Ishikaa Lunawat and Isabel Sieh and Sean Kirmani and Sergey Levine and Jiajun Wu and Chelsea Finn and Hao Su and Quan Vuong and Ted Xiao},
        journal = {arXiv preprint arXiv:2405.05941},
        year={2024},
        }
```
