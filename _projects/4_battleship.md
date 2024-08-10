---
layout: page
title: NAO Playing Battleship
description: Humanoid playing battleship against human opponent
img: assets/projects/battleship/NAO.jpg
importance: 1
category: undergrad
---

<div class="row justify-content-sm-center">
{% include video.liquid path="https://www.youtube.com/embed/N-u9TRkwQLY?si=Akzzp1N2db9x76P9" class="rounded z-depth-1" width="480px" height="360px" %}
</div>
<div class="caption">
    NAO battling against a human opponent in a game of battleship!
</div>

## About Battleship

Battleship is a classical guessing game played between two opponents [[1]](#1). Each player has
a fleet that includes several ships of different sizes. These ships are to be
positioned on a Battleship board. The Battleship board is a grid of square cells
with equal rows and columns. The position of each ship is selected by each
player without any restrictions except in the case of overlapping ships, which
is forbidden. After the positioning is finished, the game may begin, and the
position of the ships cannot be changed. The goal of this game is to sink every
enemy ship before the opponent sinks your fleet.

In each turn, a player is on the defensive and the other on the attacking end.
The one who is attacking has to guess where the opponent has positioned its
fleet, choose a board coordinate that the player wishes to hit, announce the
coordinate and wait for the other player's response. On the other hand, the
defending player has to check if the selected coordinate of the attacker has
successfully hit a ship of his fleet and then announce the results truthfully to
the opponent. For the next turn, the roles change between the players, and the
attacker becomes the defendant and vice versa. This swap of roles continues
until one of the two players is left without any non-sunken ship. A ship is
sunken if every cell it occupies has been hit. Furthermore, when a ship receives
the final hit, its owner has to announce to the opponent that it has been sunken
along with the type of this specific ship.

## Gameplay

<div class="row justify-content-md-center">
    <div class="col-sm-5 text-center">
            {% include figure.liquid path="assets/projects/battleship/board.png" title="aruco board" width="75%" class="img-fluid rounded z-depth-1" %}
        <div class="caption">
           5x5 Board with an Aruco marker on top.
        </div>
    </div>
    <div class="col-sm-7 text-center">
        {% include figure.liquid path="assets/projects/battleship/gameflow.png" title="battleship_flowchart" width="75%" class="img-fluid rounded z-depth-1" %}
        <div class="caption">
           Flowchart depicting gameplay.
        </div>
    </div>
</div>

The goal of this project is to make NAO [[2]](#2) play battleship against a human opponent. For this project, we used are 5x5 size board and each fleet constructed from 2 Destroyer ships of 3 cell size and 2 Submarine ships of 2 cell size. For NAO to play this guessing game, we devised a vision, control, voice, and cognition system. The vision system helps NAO realize and locate the game board, the control system enables NAO to place its ships on board using its arms, the voice system lets NAO interact with the human opponent, and the cognition allows NAO to reason and play the game.

## Team

Sumit Patidar, Konstantinos Theodorou

## References

<a id="1">[1]</a>
NAO humanoid. IEEE. Available at:
[https://robots.ieee.org/robots/nao/](https://robots.ieee.org/robots/nao/)
(Accessed: 5 October 2022)

<a id="2">[2]</a>
Battleship. Wikipedia. Available at:
[https://en.wikipedia.org/wiki/Battleship\_(game)](<https://en.wikipedia.org/wiki/Battleship_(game)>)
(Accessed: 5 October 2022)
