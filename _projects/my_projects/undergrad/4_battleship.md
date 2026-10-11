---
layout: page
title: Battleship
description: Humanoid robot battleship player
img: assets/projects/undergrad/battleship/NAO.jpg
importance: 4
category: undergrad
---

<div class="row justify-content-md-center">
    <div class="col-10">
    {% include video.liquid path="https://www.youtube.com/embed/N-u9TRkwQLY?si=Akzzp1N2db9x76P9" class="rounded z-depth-1" %}
    </div>
</div>

<div class="caption">
    NAO battling against a human opponent in a game of battleship!
</div>

## Overview

Developed a complete robotic system that enables a NAO humanoid robot to
autonomously play Battleship against a human opponent. The project was
completed during my semester exchange at the **Technical University of Munich
(TUM), Germany**.

The robot had to visually locate and understand the game board, physically
place its ships using its arms, communicate with the human player through
speech, and reason about previous moves to select subsequent attacks.

---

## My Contributions

- **Vision:** Developed the board detection and localization pipeline using
  ArUco markers, enabling the robot to identify the physical game board and
  establish its coordinate frame.
- **Control & Manipulation:** Developed the robot arm control and manipulation
  required for the robot to physically place and interact with ships on the
  board.
- **Voice Interaction:** Implemented components of the voice-based interaction
  system, enabling the robot to communicate game actions and results with the
  human player.
- **System Integration:** Integrated the perception, control, manipulation, and
  voice components into the overall autonomous gameplay pipeline.

---

## System

The system was organized into four main components:

- **Vision:** Detected and localized the Battleship board using an ArUco marker,
  providing a consistent reference frame for the robot.
- **Manipulation:** Planned and executed arm movements to physically place the
  robot's ships onto the board.
- **Voice Interaction:** Enabled the robot to communicate with the human opponent,
  including announcing moves and responding to hits, misses, and sunk ships.
- **Game Cognition:** Maintained the game state, tracked previously attempted
  coordinates, reasoned about the opponent's fleet, and selected subsequent
  moves.

The game was implemented on a 5×5 board with a fleet consisting of two 3-cell
Destroyers and two 2-cell Submarines.

The overall system follows a: **Vision →
State Estimation → Decision Making → Control & Manipulation → Voice
Interaction** loop, allowing the robot to perceive and interact with the
physical game environment while playing against a human opponent.

<div class="row justify-content-md-center">
    <div class="col-sm-5 text-center">
            {% include figure.liquid path="assets/projects/undergrad/battleship/board.png" title="aruco board" width="75%" class="img-fluid rounded z-depth-1" %}
        <div class="caption">
           5x5 Board with an Aruco marker on top.
        </div>
    </div>
    <div class="col-sm-7 text-center">
        {% include figure.liquid path="assets/projects/undergrad/battleship/gameflow.png" title="battleship_flowchart" width="75%" class="img-fluid rounded z-depth-1" %}
        <div class="caption">
           Flowchart depicting gameplay.
        </div>
    </div>
</div>

---

## Technical Highlights

- **Platform:** NAO humanoid robot
- **Perception:** ArUco marker detection + board localization
- **Calibration:** Board-to-robot coordinate transformation
- **Motion & Control:** Arm motion control for physical interaction
- **Manipulation:** Autonomous ship placement on a physical board
- **HRI:** Voice-based interaction with human opponent
- **Planning:** Game-state tracking + autonomous move selection
- **Integration:** End-to-end perception, planning, control, manipulation, and HRI pipeline

---

## Team

**Sumit Patidar · Konstantinos Theodorou**

---

## References

<a id="1">[1]</a>
NAO humanoid. IEEE. Available at:
[https://robots.ieee.org/robots/nao/](https://robots.ieee.org/robots/nao/)
(Accessed: 5 October 2022)

<a id="2">[2]</a>
Battleship. Wikipedia. Available at:
[https://en.wikipedia.org/wiki/Battleship\_(game)](<https://en.wikipedia.org/wiki/Battleship_(game)>)
(Accessed: 5 October 2022)
