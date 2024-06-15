---
layout: page
title: Cubinator
description: The Rubik's cube solving robot
img: assets/img/projects/cubinator.gif
importance: 1
category: undergrad
related_publications: false
---

<div class="row justify-content-sm-center">
{% include video.liquid path="https://www.youtube.com/embed/UdD4uY8Ph30?si=VLm4GNRUDZhBfgLY" class="rounded z-depth-1" width="480px" height="360px" %}
</div>
<div class="caption">
    Cubinator in action!
</div>

## The Rise of Cubinator

I was in the 2nd semester of my bachelor's and had been practicing to solve a 3x3 Rubik's cube quickly for the last few months. My two roommates, Utkarsh and Versha, inspired me to take up Rubik's cube solving. Those two geniuses could already solve a variety of Rubik's cubes, some under less than 20 seconds! During that time, we all were enrolled in an Electronics coursework. As part of one of our assignments, we were required to build any working prototype under $20. Since all three of us could solve a 3x3 Rubik's cube, we thought, why not also make a robot that could solve a Rubik's cube? We challenged ourselves and completed the project in about 2-3 months. Through this project, I set my foot in the world of electronics, motors, microcontrollers, and fabrication.

## How Cubinator Works?

Cubinator is an Arduino-powered Rubik's cube-solving robot. It takes the cube's initial configuration as a sequence of color tiles on each side of the cube. It then uses God's algorithm [[1]](#1) to output a series of required cube rotations aimed at solving a Rubik's cube. These rotations are executed via Arudino by controlling DC and servo motors in an open loop. The average time of solving any given configuration is about two minutes.

We planned to use the smartphone camera to detect the colors on each side of the cube. However, there was inconsistency in detecting red and orange colors in different lighting conditions. Since we couldn't resolve the issue in time, we resorted to manually inputting the color sequence through a laptop connected to the Arduino. God's algorithm processed the input configuration on the laptop, and the cube rotations were sent to the Arduino in a sequence. We also 3D-printed our custom rack and pinion gears, and the claws to hold and rotate the Rubik's cube sides.

## Team

Sumit Patidar, Utkarsh Kunwar, Versha Dhankar, Vipin Tolia, Shubham

## References

<a id="1">[1]</a>
God's algorithm. Wikipedia. Available at:
[https://en.wikipedia.org/wiki/God%27s_algorithm ](https://en.wikipedia.org/wiki/God%27s_algorithm)
(Accessed: 5 October 2022)
