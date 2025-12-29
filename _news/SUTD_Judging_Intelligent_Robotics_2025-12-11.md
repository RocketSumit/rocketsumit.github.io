---
layout: post
title: Judging Intelligent Robotics (30.119) at SUTD 🤖
date: 2025-12-11 21:00:00+0800
inline: false
related_posts: true
---

<div class="row align-items-start my-4">

<!-- Left column: Content -->
<div class="col-md-6">
    <p>
        I had the opportunity to support the judging session for the course
        <strong>30.119 Intelligent Robotics</strong> at the Singapore University of
        Technology and Design (SUTD) on <strong>11 December 2025</strong>. Participating
        as a volunteer with the <strong>James Dyson Foundation</strong>, I assisted
        in evaluating the students’ final robotics projects.
    </p>
    <p>
        The session, held from <strong>11:30 AM to 2:00 PM</strong>, marked the
        culmination of several weeks of hands-on learning, where students designed,
        built, and deployed autonomous robotic systems using <strong>ROS 2</strong>.
        It was a showcase of their technical depth, problem-solving skills, and
        growing confidence in real-world robotics development.
    </p>

    <ul>
      <li><a href="#course-overview">Course Overview</a></li>
      <li><a href="#the-challenge--presentations">The Challenge & Presentations</a></li>
      <li><a href="#technology-stack">Technology Stack</a></li>
      <li><a href="#judging-criteria">Judging Criteria</a></li>
      <li><a href="#my-experience">My Experience</a></li>
    </ul>
  </div>

 <!-- Right column: Video -->
  <div class="col-md-6 mb-3 mb-md-0">
    {% include video.liquid
      path="assets/blogs/jdf_sutd_intelligent_robots/sutd-intelligent-robots-course-comp.mp4"
      class="img-fluid rounded z-depth-1"
      controls=true
      autoplay=true
    %}
  </div>
</div>

## Course Overview

The **30.119 Intelligent Robotics** course is designed to give students practical exposure to real-world robotic systems, with a strong emphasis on autonomy and software integration.

**Key details:**

- **Learning Objective:**
  Build an autonomous robot capable of overcoming a mini challenge, with a focus on ROS 2 capabilities such as navigation, mapping, and exploration.
- **Students & Teams:**
  26 students divided into 7 teams.
- **Student Profile:**
  Term 7 undergraduate students enrolled in 30.119 Intelligent Robotics.
- **Venue:**
  Dyson–SUTD Innovation Studios
- **Point of Contact:**
  [Asst. Prof. U-Xuan](https://www.sutd.edu.sg/profile/tan-u-xuan/)

## The Challenge & Presentations

The live demo was split into **two parts**.

### Part 1: Autonomous Navigation & Perception

Teams had to demonstrate the **navigation capability** of a TurtleBot in a structured indoor environment:

- Navigate through a sequence of predefined **waypoints**
- Stop navigating when encountering **stop signs**
- Enter different rooms and **count the number of intruders**
- Intruders were represented by **photos of people pasted on the walls**
- Identify and localize intruders, visualizing them in **RViz**
- Return the robot safely to the **start pose**

### Part 2 (Bonus): Autonomous Exploration & Mapping

As a bonus task, teams attempted to:

- Autonomously **explore the environment**
- Build a **map** using exploration strategies
- Optimize both **map coverage** and **time taken**

Each team was given **10 minutes** to complete both the main and bonus tasks.

## Technology Stack

The students worked with a solid and industry-relevant robotics stack:

- **Navigation:**
  ROS 2 Nav2
- **Perception:**
  YOLO for intruder (person) detection
- **Exploration & Mapping:**
  Frontier-based exploration using
  <https://github.com/AniArka/Autonomous-Explorer-and-Mapper-ros2-nav2>

It was great to see students integrate multiple subsystems—navigation, perception, and mapping—into a cohesive autonomous pipeline.

## Judging Criteria

The evaluation focused on both **performance** and **robustness**:

- Successful navigation through all waypoints
- Correct detection and counting of intruders
- Accurate localization of intruders in RViz
- Ability to return to the start pose
- **Time taken** to complete the tasks

For the bonus round:

- Amount of map coverage achieved
- Time taken to build the map autonomously

## My Experience

The atmosphere during the judging was a mix of **nervous energy and excitement**. Some teams executed their pipelines smoothly, while others faced last-minute glitches—very much reflective of real-world robotics deployments.

What stood out was the competitive yet enthusiastic spirit. Students were eager to **beat each other’s completion times** and climb the leaderboard, cheering on successful runs and learning quickly from failures. Despite the pressure of the 10-minute limit, the teams showed strong problem-solving skills and resilience.

Overall, it was a fun and rewarding experience to judge these projects. Sessions like this are incredibly motivating for students and serve as a strong foundation for taking on more **advanced robotics courses and research** in the future. It was inspiring to see how far they’ve come in building intelligent, autonomous systems within a single course.
