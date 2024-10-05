---
layout: post
title: Path Planning Algorithms
date: 2024-09-28 09:30:00
description: Review of some popular path planning algorithms in robotics
tags: code
categories: robotics
---

In this blog post, I try to summarize some of the popularly used path planning algorithms in robotics.

- [Non-Sampling-Based Algorithms](#non-sampling-based-algorithms)
  - [Dijkstra](#dijkstra)
  - [A\*](#a)
- [Sampling-Based Algorithms](#sampling-based-algorithms)
  - [RRT](#rrt)
  - [RRT\*](#rrt-1)
  - [PRM](#prm)

# Non-Sampling-Based Algorithms

## Dijkstra

A Greedy algorithm for finding the shortest path in a graph. It explores all nodes in all directions equally (like breadth-first search).

```python
Input: Graph (nodes, edges), start, goal

# Initialize
Distance to all nodes n, D[n] = inf
Nodes to visit (priority-queue), V = all nodes
D[start] = 0
parent node pair = empty

while V != empty
    u = pop(V) # get the node with minimum distance to start
    for all neighbours of u as v
        if E(u,v) + D[u] < D[v]
            update parent(v) = u

# Get the path from start to goal
target = goal
u = parent(u)
path = []

while parent[u] or u = source
    path.insert(0, u) # insert at beginning of list
    u = parent(u)
```

## A\*

Very similar to Dijkstra, but is heuristic driven i.e uses both the cost and estimated cost (heuristics) to reach current node. The heuristic helps guide the search towards the goal, making it more efficient.

```python
# add heuristics (H) to the cost
E(u,v) + H(u,v) + D[u]< D[v]
```

# Sampling-Based Algorithms

## RRT

Rapidly exploring random trees (RRT) is a sampling based algorithm which incrementally builds a tree to efficiently sample high-dimensional spaces. RRT (even with more iterations) is not guaranteed to find a optimal path.

```python

Input: start, goal, max_iters, step_size

# Initialize
tree = [start] # tree root with start node

for i in range(max_iters):
  rand_point = sample_random_point()  # Randomly sample a point in the space
  nearest_node = find_nearest(tree, rand_point)  # Find the nearest node in the tree
  new_node = steer(nearest_node, rand_point, step_size)  # Move towards the random point

  if not collision_check(nearest_node, new_node):  # Check for collisions
    tree.append(new_node)  # Add the new node to the tree
  if distance(new_node, goal) < threshold:  # Check if close to goal
    return construct_path(tree, start, goal)  # Return the path to goal

return None  # No path found
```

## RRT\*

RRT* finds the optimal path by adding two more steps to RRT. 1) When adding a new node, choose the best parent for that node 2) rewire the entire tree i.e choose the best parent for entire tree. If given more iterations, RRT* is gauranteed to converge unlike RRT.

```python
# Initialize
tree = [start] # tree root with start node

for i in range(max_iters):
  rand_point = sample_random_point()  # Randomly sample a point in the space
  nearest_node = find_nearest(tree, rand_point)  # Find the nearest node in the tree
  new_node = steer(nearest_node, rand_point, step_size)  # Move towards the random point

  if not collision_check(nearest_node, new_node):  # Check for collisions
    # Choose the best parent for new_node
    best_parent = choose_best_parent(tree, new_node)
    tree.append(new_node)  # Add the new node to the tree
    # Rewire the tree to improve path quality
    rewire(tree, new_node)

  if distance(new_node, goal) < threshold:  # Check if close to goal
    return construct_path(tree, start, goal)  # Return the path to goal

return None  # No path found
```

## PRM

Probabilistic Roadmap (PRM) is a multi-query algorithm that constructs a graph (roadmap) by randomly sampling points from the environment and connecting them if they are close and collision-free. It is mainly used to efficiently explore paths in high-dimensional spaces. Once the graph is built, queries can be made to find paths between a start and goal point using search algorithms.

```python
Input: num_samples, k, start, goal

# Initialize
roadmap = []  # empty roadmap (graph)

# Phase 1: Roadmap Construction
for i in range(num_samples):
  sample = sample_random_point()  # Sample free space
  roadmap.append(sample)

  neighbors = find_nearest_neighbors(roadmap, sample, k)  # Find k nearest neighbors

  for neighbor in neighbors:
    if not collision_check(sample, neighbor):
    add_edge(roadmap, sample, neighbor)

# Phase 2: Path query
# Step 1: Connect start and goal to the roadmap
start_neighbors = find_nearest_neighbors(roadmap, start, k)  # Find start neighbors
goal_neighbors = find_nearest_neighbors(roadmap, goal, k)    # Find goal neighbors

for neighbor in start_neighbors:
    if not collision_check(start, neighbor):
        add_edge(roadmap, start, neighbor)
for neighbor in goal_neighbors:
    if not collision_check(goal, neighbor):
        add_edge(roadmap, goal, neighbor)

# Step 2: Use graph search algorithm to find path
path = graph_search(roadmap, start, goal)  # A* or Dijkstra's algorithm
return path if path else None  # Return path if found, otherwise None
```
