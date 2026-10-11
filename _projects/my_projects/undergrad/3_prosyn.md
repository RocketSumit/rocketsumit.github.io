---
layout: page
title: ProSynn
description: An educational game for learning protein synthesis through interactive gameplay.
img: assets/projects/undergrad/prosyn/prosynn_logo.png
importance: 3
category: undergrad
---

<div class="row justify-content-md-center align-items-center">

    <!-- Left column: Video -->
    <div class="col-md-4 mb-4 mb-md-0">
        {% include video.liquid
            path="assets/projects/undergrad/prosyn/gameplay.mp4"
            class="img-fluid rounded z-depth-1"
            controls=true
            autoplay=true
        %}
        <div class="caption text-center">
            Gameplay Video
        </div>
    </div>

    <!-- Right column: 4 screenshots -->
    <div class="col-md-4">

        <div class="row">

            <div class="col-6 mb-3">
                {% include figure.liquid
                    path="assets/projects/undergrad/prosyn/gameplay_1.png"
                    title="ProSynn gameplay"
                    width="100%"
                    class="img-fluid rounded z-depth-1"
                %}
            </div>

            <div class="col-6 mb-3">
                {% include figure.liquid
                    path="assets/projects/undergrad/prosyn/gameplay_2.png"
                    title="ProSynn gameplay"
                    width="100%"
                    class="img-fluid rounded z-depth-1"
                %}
            </div>

            <div class="col-6">
                {% include figure.liquid
                    path="assets/projects/undergrad/prosyn/gameplay_3.png"
                    title="ProSynn gameplay"
                    width="100%"
                    class="img-fluid rounded z-depth-1"
                %}
            </div>

            <div class="col-6">
                {% include figure.liquid
                    path="assets/projects/undergrad/prosyn/gameplay_4.png"
                    title="ProSynn gameplay"
                    width="100%"
                    class="img-fluid rounded z-depth-1"
                %}
            </div>

        </div>

        <div class="caption text-center">
            ProSynn application screenshots
        </div>

    </div>

</div>

## Overview

**ProSynn** is an interactive educational game designed to make learning
**protein synthesis** more engaging through gameplay.

Developed during my undergraduate biotechnology studies, the application
transforms the biological process of **translation** into a timed game. Players
match mRNA codons with their corresponding amino acids to synthesize proteins
while managing a limited number of mistakes.

The application was developed using the **Unity game engine** and deployed
across **Android, Windows, and Linux**.

---

## My Contributions

- Designed and developed the complete educational game from concept to implementation.
- Translated the biological process of protein synthesis into interactive gameplay mechanics.
- Implemented the game logic, scoring, timers, and player feedback.
- Designed the user interaction and visual presentation of the application.
- Developed and packaged the application for multiple platforms.

---

## System

The game focuses on the **translation stage of protein synthesis**.

Players are presented with mRNA codons and must correctly identify the
corresponding amino acids. Correct matches contribute toward protein synthesis,
while incorrect choices consume one of the player's limited attempts.

The game supports **10, 20, and 30-second** gameplay modes, with the objective
of synthesizing as many proteins as possible within the selected time limit.

The core gameplay loop is:

**mRNA Codon → Amino Acid Selection → Correct/Incorrect Feedback → Protein
Synthesis → Score**

Players are allowed a maximum of **two mistakes** before the game ends.

---

## Technical Highlights

- **Engine:** Unity 5.4.2f2
- **Platforms:** Android, Windows, Linux
- **Domain:** Biotechnology / Educational Technology
- **Core Mechanic:** mRNA codon → amino acid matching
- **Gameplay:** Timed protein synthesis challenge
- **Game Modes:** 10, 20, and 30 seconds
- **Game Logic:** Scoring, mistake tracking, timers, and game-state management
- **Educational Focus:** Interactive learning of protein translation

---

## Team

**Sumit Patidar · Archit · Vaibhav**
