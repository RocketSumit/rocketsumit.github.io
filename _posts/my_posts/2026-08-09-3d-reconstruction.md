---
layout: post
title: "3D Reconstruction: From Pixels to Radiance Fields"
date: 2026-08-09 10:00:00
description: "How computers turn flat 2D photographs into rich 3D worlds: from voxels and meshes to NeRF and 3D Gaussian Splatting."
tags: [ml, computer-vision, robotics]
categories: tech
related_posts: false
---

Imagine walking around a wooden park bench, snapping a dozen photos on your phone.

Your brain effortlessly synthesizes these 2D snapshots into a continuous 3D mental model. You instinctively know where the bench ends, how far the bicycle rests behind it, and what the scene looks like from angles you never directly captured.

<div class="row justify-content-md-center">
  <div class="col-sm-6 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/02-multiple-views.jpg" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">Multi-view captures: the raw input required to infer spatial relationships.</div>
  </div>
  <div class="col-sm-6 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/01-3d-view-generation.gif" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">3D render of the scene.</div>
  </div>
</div>

A computer gets none of this for free. To an algorithm, an image is just a flat 2D grid of RGB values. Reconstructing physical 3D reality from 2D images is the core challenge of **3D Reconstruction** and **Novel-View Synthesis**. Today, this technology underpins robotics, spatial computing, VFX, and digital twins.

Let's unpack how we solve this fundamental problem—and explore how representations evolved from rigid geometric meshes to modern neural radiance fields and 3D Gaussian splats.

- [The Core Challenge: An Ill-Posed Inverse Problem](#the-core-challenge-an-ill-posed-inverse-problem)
- [Classical 3D Scene Representations](#classical-3d-scene-representations)
  - [1. Voxels: Space as Discrete Cubes](#1-voxels-space-as-discrete-cubes)
  - [2. Point Clouds: Sparse Coordinates](#2-point-clouds-sparse-coordinates)
  - [3. Polygon Meshes: The Graphics Standard](#3-polygon-meshes-the-graphics-standard)
- [The Foundation: Structure-from-Motion (SfM)](#the-foundation-structure-from-motion-sfm)
- [Implicit Neural Representations: NeRF](#implicit-neural-representations-nerf)
  - [Differentiable Volume Rendering](#differentiable-volume-rendering)
  - [The NeRF Bottleneck](#the-nerf-bottleneck)
- [Explicit Neural Splatting: 3D Gaussian Splatting (3DGS)](#explicit-neural-splatting-3d-gaussian-splatting-3dgs)
  - [Tile-Based Rasterization: Real-Time Performance](#tile-based-rasterization-real-time-performance)
- [Head-to-Head: NeRF vs. 3D Gaussian Splatting](#head-to-head-nerf-vs-3d-gaussian-splatting)
- [Why 3D Representations Matter for Robotics](#why-3d-representations-matter-for-robotics)
- [Key Takeaways](#key-takeaways)
- [Further Reading](#further-reading)

---

## The Core Challenge: An Ill-Posed Inverse Problem

Why is 3D vision hard? Because taking a photograph is a **lossy projection**:

$$\mathbb{R}^3 \xrightarrow{\text{Perspective Projection}} \mathbb{R}^2$$

When a 3D point projects onto a 2D pixel, **depth is permanently discarded**. A single red pixel could originate from an object 1 meter away or a massive structure 100 meters away.

<div class="row justify-content-md-center">
  <div class="col-sm-8 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/03-2d-image.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">A 2D pixel array captures color $(R, G, B)$ but completely loses the metric depth $(Z)$ dimension.</div>
  </div>
</div>

Recovering 3D geometry from 2D images is an **ill-posed inverse problem**: infinitely many 3D configurations can project onto the exact same set of 2D images. Resolving this ambiguity requires choosing the right mathematical representation of space.

---

## Classical 3D Scene Representations

Before neural representations existed, vision systems relied on explicit geometric structures—each bringing critical trade-offs.

### 1. Voxels: Space as Discrete Cubes

The simplest approach divides 3D space into a uniform volumetric grid (think _Minecraft_).

<div class="row justify-content-md-center">
  <div class="col-sm-8 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/04-voxels.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">Dense voxel grids: simple occupancy reasoning crippled by cubic memory scaling.</div>
  </div>
</div>

- **The Drawback:** Cubic complexity $\mathcal{O}(N^3)$. Doubling the resolution consumes $8\times$ more memory. Most voxel memory is wasted storing empty air.

---

### 2. Point Clouds: Sparse Coordinates

Instead of empty grids, store an unordered set of 3D spatial points:

$$\mathcal{} = \{p_i \in \mathbb{R}^3 \mid i = 1, \dots, N\}$$

Sensors like LiDAR and depth cameras naturally produce point clouds.

<div class="row justify-content-md-center">
  <div class="col-sm-8 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/05-point-cloud.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">A point cloud: memory-efficient coordinates that lack continuous surface connectivity.</div>
  </div>
</div>

- **The Drawback:**
  - **The "Screen-Door" Effect:** Because points lack surface area, zooming in or viewing from grazing angles reveals gaps and background bleed-through.
  - **No Surface Normals or Occlusion:** Points do not encode topology, making realistic lighting and solid surface rendering difficult.

---

### 3. Polygon Meshes: The Graphics Standard

Meshes explicitly define continuous surfaces using collections of **vertices, edges, and triangular faces**.

<div class="row justify-content-md-center">
  <div class="col-sm-8 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/06-mesh.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">Triangular surface meshes: fast GPU rasterization, but difficult to optimize from images.</div>
  </div>
</div>

Meshes are the backbone of real-time graphics engines, but extracting clean meshes via traditional multi-view photogrammetry breaks down on complex real-world materials:

- **Fuzziness & Hair:** Thin strands, fur, and tree leaves cannot be modeled cleanly by rigid polygons without millions of degenerate micro-triangles.
- **Transparency & Volumetrics:** Smoke, glass, water, and fog have no singular hard boundary.
- **Rigidity & Non-Manifold Artifacts:** Optimization algorithms struggle to handle sharp topological changes or self-occluding boundaries.

<div class="row justify-content-md-center">
  <div class="col-sm-10 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/07-summary.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">Trade-off comparison: geometric precision, volumetric handling, and rendering overhead.</div>
  </div>
</div>

---

## The Foundation: Structure-from-Motion (SfM)

Regardless of whether we use traditional or neural rendering, every pipeline begins with camera calibration. If we do not know the precise location of each camera in 3D space, inverse rendering is impossible.

<div class="row justify-content-md-center">
  <div class="col-sm-8 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/09-multi-view-input.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">Calibrated multi-view inputs: computing camera matrices is the initial prerequisite.</div>
  </div>
</div>

**Structure-from-Motion (SfM)** recovers camera extrinsic parameters ($R, \mathbf{t}$), intrinsic parameters, and a sparse point cloud using a 4-step pipeline:

1. **Feature Detection & Matching:** Identify distinctive visual landmarks (e.g., SIFT, SuperPoint) across images.
2. **Epipolar Geometry:** Calculate essential and fundamental matrices to derive relative camera motions.
3. **Triangulation:** Cast intersecting rays from matched features to calculate initial 3D positions.
4. **Bundle Adjustment:** Jointly optimize camera poses $\mathbf{}_i$ and 3D points $\mathbf{}_j$ by minimizing reprojection error across all views:

$$\min_{\{\mathbf{}_i\}, \{\mathbf{}_j\}} \sum_{i,j} \left\| \mathbf{}_{i,j} - \pi(\mathbf{}_i, \mathbf{}_j) \right\|^2$$

<div class="row justify-content-md-center">
  <div class="col-sm-4 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/10-sfm_01.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">1. Keypoint matching across overlapping views.</div>
  </div>
  <div class="col-sm-4 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/10-sfm_02.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">2. Pairwise camera pose estimation.</div>
  </div>
  <div class="col-sm-4 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/10-sfm_03.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">3. Global bundle adjustment refinement.</div>
  </div>
</div>

---

## Implicit Neural Representations: NeRF

What if we stop storing explicit geometry (points/triangles) altogether and instead **store the entire scene inside the weights of a neural network**?

<div class="row justify-content-md-center">
  <div class="col-sm-8 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/08-nerf-intuition.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">NeRF encodes continuous density and view-dependent color within a multi-layer perceptron.</div>
  </div>
</div>

Introduced in 2020, **Neural Radiance Fields (NeRF)** parameterize a scene as a continuous 5D function parameterized by a Multi-Layer Perceptron (MLP):

$$F_\Theta: (x, y, z, \theta, \phi) \longrightarrow (\mathbf{}, \sigma)$$

- **$(x, y, z)$:** 3D coordinates in space
- **$(\theta, \phi)$:** 2D viewing direction vector $\mathbf{d}$
- **$\mathbf{} = (r, g, b)$:** Emitted RGB radiance
- **$\sigma$:** Volumetric density (opacity/thickness)

### Differentiable Volume Rendering

To render a pixel, NeRF casts a camera ray $\mathbf{r}(t) = \mathbf{o} + t\mathbf{d}$ through the scene, samples discrete points along the ray, queries the MLP for color and density, and composites them:

$$C(\mathbf{r}) = \int_{t_n}^{t_f} T(t) \sigma(\mathbf{r}(t)) \mathbf{}(\mathbf{r}(t), \mathbf{d}) \, dt, \quad \text{where } T(t) = \exp\left(-\int_{t_n}^{t} \sigma(\mathbf{r}(s)) \, ds\right)$$

<div class="row justify-content-md-center">
  <div class="col-sm-8 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/11-nerf-training.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">Ray-marching pipeline: samples along each camera ray are aggregated into synthetic pixel colors.</div>
  </div>
</div>

Because every step of this numerical integration is differentiable, we optimize network weights directly via gradient descent on a photometric loss:

$$\mathcal{}_{\text{photo}} = \sum_{\mathbf{r} \in \mathcal{R}} \left\| C(\mathbf{r}) - C_{\text{gt}}(\mathbf{r}) \right\|_2^2$$

### The NeRF Bottleneck

While NeRF handles fine hair, reflections, and smoke with ease, **rendering is painfully slow**. Generating a single $1920 \times 1080$ frame requires evaluating the MLP hundreds of millions of times, making real-time interactive rendering difficult without extensive acceleration tricks.

---

## Explicit Neural Splatting: 3D Gaussian Splatting (3DGS)

In 2023, **3D Gaussian Splatting** addressed NeRF's computational bottleneck by abandoning MLPs in favor of explicit, differentiable primitives.

<div class="row justify-content-md-center">
  <div class="col-sm-8 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/12-3dgs-overview.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">3DGS: representing scenes as millions of parameterized 3D ellipsoids.</div>
  </div>
</div>

Instead of querying a neural network for every point along a ray, 3DGS models the world as millions of 3D Gaussians:

$$
G(\mathbf{x}) =
\exp\left(
-\frac{1}{2}
(\mathbf{x}-\boldsymbol{\mu})^\top
\Sigma^{-1}
(\mathbf{x}-\boldsymbol{\mu})
\right)
$$

where:

- $\mathbf{x} \in \mathbb{R}^3$ is a point in 3D space.
- $\boldsymbol{\mu} \in \mathbb{R}^3$ is the Gaussian's center.
- $\Sigma \in \mathbb{R}^{3\times3}$ is the covariance matrix, which determines its scale and orientation.

Each primitive maintains:

1. **Position ($\boldsymbol{\mu}$):** 3D center $(x, y, z)$
2. **Covariance ($\Sigma$):** Decomposed into rotation quaternion $q$ and 3D scale vector $s$ ($\Sigma = R S S^\top R^\top$) to guarantee positive semi-definiteness
3. **Opacity ($\alpha$):** Volumetric density
4. **Color:** Modeled via Spherical Harmonics (SH) coefficients to capture view-dependent specular highlights

<div class="row justify-content-md-center">
  <div class="col-sm-8 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/13-3dgs-antomy.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">Anatomy of a Gaussian primitive: position, scale, orientation, opacity, and view-dependent color.</div>
  </div>
</div>

### Tile-Based Rasterization: Real-Time Performance

3DGS replaces slow ray-marching with GPU-accelerated rasterization:

1. **Projection:** Project 3D Gaussians into 2D screen-space ellipses using a local affine approximation.
2. **Tile Sorting:** Partition the screen into $16 \times 16$ pixel tiles and fast-sort the Gaussians by depth (using radix sort).
3. **$\alpha$-Blending:** Blend the overlapping Gaussians in front-to-back order within each tile in parallel.

<div class="row justify-content-md-center">
  <div class="col-sm-8 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/14-tile-rasterizer.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">Tile-based rasterization: GPU-native parallel sorting and alpha blending enables 100+ FPS rendering.</div>
  </div>
</div>

<div class="row justify-content-md-center">
  <div class="col-sm-8 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/15-3dgs-training.png" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">The 3DGS optimization loop: dynamic splitting, pruning, and density adjustments over time.</div>
  </div>
</div>

---

## Head-to-Head: NeRF vs. 3D Gaussian Splatting

| Dimension                    |   Neural Radiance Fields (NeRF)    |      3D Gaussian Splatting (3DGS)       |
| :--------------------------- | :--------------------------------: | :-------------------------------------: |
| **Representation**           | 🧠 Implicit — Neural Network / MLP |       🟢 Explicit — 3D Gaussians        |
| **Rendering Engine**         |          🐢 Ray Marching           | ⚡ Tile-Based Splatting & Rasterization |
| **Rendering Speed**          |            ❌ 0.1–5 FPS            |           ✅ **100–200+ FPS**           |
| **Training Time**            |          ❌ Hours to Days          |          ✅ **15–45 Minutes**           |
| **Memory Footprint**         |       ✅ Compact<br>~5–50 MB       |       ❌ Higher<br>~200 MB–1.5 GB       |
| **Fluffy / Thin Structures** |            ✅ Excellent            |              ✅ Excellent               |
| **Real-Time Rendering**      |           ❌ Challenging           |               ✅ **Yes**                |
| **Photorealistic Quality**   |            ✅ Excellent            |              ✅ Excellent               |

---

## Why 3D Representations Matter for Robotics

A physical robot cannot plan trajectories in flat pixel space. It needs persistent spatial representations to handle contact dynamics, obstacle avoidance, and manipulation.

<div class="row justify-content-md-center">
  <div class="col-sm-8 text-center">
    {% include figure.liquid path="./assets/blogs/3d-reconstruction/17-robotics-application.jpeg" width="100%" class="img-fluid rounded z-depth-1" %}
    <div class="caption text-center">3D representations provide spatial context for robot manipulation, path planning, and physics simulation.</div>
  </div>
</div>

- **Dense Spatial Reasoning:** Knowing unoccupied free space vs. solid collision boundaries.
- **Novel View Synthesis for Simulation:** Generating synthetic training rollouts for visuomotor policy learning without running thousands of real-world trials.
- **Differentiable Physics Interfaces:** Coupling explicit representations like 3DGS with physical simulators to perform real-time robot grasp planning and visual tracking.

---

## Key Takeaways

1. **3D reconstruction is an ill-posed inverse problem** because 2D projections discard absolute depth and introduce occlusions.
2. **Meshes struggle with complex materials** like smoke, fur, and thin structures; **point clouds suffer from the screen-door effect**.
3. **NeRF introduced continuous neural volumetric rendering**, solving fuzziness and specularities at the cost of high rendering latency.
4. **3D Gaussian Splatting delivers the best of both worlds**: explicit volumetric primitives optimized end-to-end and rendered at real-time frame rates via GPU rasterization.

---

## Further Reading

- [NeRF: Representing Scenes as Neural Radiance Fields for View Synthesis](https://arxiv.org/abs/2003.08934) (Mildenhall et al., ECCV 2020)
- [3D Gaussian Splatting for Real-Time Radiance Field Rendering](https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/) (Kerbl et al., SIGGRAPH 2023)
- [Structure-from-Motion Revisited](https://demuc.de/papers/schoenberger2016sfm.pdf) (Schönberger & Frahm, CVPR 2016)
- [COLMAP Documentation](https://colmap.github.io/) — The standard open-source library for SfM and multi-view reconstruction.
