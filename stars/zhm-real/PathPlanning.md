---
project: PathPlanning
stars: 8943
description: Common used path planning algorithms with animations.
url: https://github.com/zhm-real/PathPlanning
---

Overview
--------

This repository implements some common path planning algorithms used in robotics, including Search-based algorithms and Sampling-based algorithms. We designed animation for each algorithm to display the running process. The related papers are listed in Papers.

Directory Structure
-------------------

```
.
└── Search-based Planning
    ├── Breadth-First Searching (BFS)
    ├── Depth-First Searching (DFS)
    ├── Best-First Searching
    ├── Dijkstra's
    ├── A*
    ├── Bidirectional A*
    ├── Anytime Repairing A*
    ├── Learning Real-time A* (LRTA*)
    ├── Real-time Adaptive A* (RTAA*)
    ├── Lifelong Planning A* (LPA*)
    ├── Dynamic A* (D*)
    ├── D* Lite
    └── Anytime D*
└── Sampling-based Planning
    ├── RRT
    ├── RRT-Connect
    ├── Extended-RRT
    ├── Dynamic-RRT
    ├── RRT*
    ├── Informed RRT*
    ├── RRT* Smart
    ├── Anytime RRT*
    ├── Closed-Loop RRT*
    ├── Spline-RRT*
    ├── Fast Marching Trees (FMT*)
    └── Batch Informed Trees (BIT*)
└── Papers
```

Animations - Search-Based
-------------------------

### Best-First & Dijkstra

### A\* and A\* Variants

Animation - Sampling-Based
--------------------------

### RRT & Variants

Papers
------

### Search-base Planning

-   A\*: A Formal Basis for the heuristic Determination of Minimum Cost Paths
-   Learning Real-Time A\*: Learning in Real-Time Search: A Unifying Framework
-   Real-Time Adaptive A\*: Real-Time Adaptive A\*
-   Lifelong Planning A\*: Lifelong Planning A\*
-   Anytime Repairing A\*: ARA\*: Anytime A\* with Provable Bounds on Sub-Optimality
-   D\*: Optimal and Efficient Path Planning for Partially-Known Environments
-   D\* Lite: D\* Lite
-   Field D\*: Field D\*: An Interpolation-based Path Planner and Replanner
-   Anytime D\*: Anytime Dynamic A\*: An Anytime, Replanning Algorithm
-   Focussed D\*: The Focussed D\* Algorithm for Real-Time Replanning
-   Potential Field, \[PPT\]: Real-Time Obstacle Avoidance for Manipulators and Mobile Robots
-   Hybrid A\*: Practical Search Techniques in Path Planning for Autonomous Driving

### Sampling-based Planning

-   RRT: Rapidly-Exploring Random Trees: A New Tool for Path Planning
-   RRT-Connect: RRT-Connect: An Efficient Approach to Single-Query Path Planning
-   Extended-RRT: Real-Time Randomized Path Planning for Robot Navigation
-   Dynamic-RRT: Replanning with RRTs
-   RRT\*: Sampling-based algorithms for optimal motion planning
-   Anytime-RRT\*: Anytime Motion Planning using the RRT\*
-   Closed-loop RRT\* (CL-RRT\*): Real-time Motion Planning with Applications to Autonomous Urban Driving
-   Spline-RRT\*: Optimal path planning based on spline-RRT\* for fixed-wing UAVs operating in three-dimensional environments
-   LQR-RRT\*: Optimal Sampling-Based Motion Planning with Automatically Derived Extension Heuristics
-   RRT#: Use of Relaxation Methods in Sampling-Based Algorithms for Optimal Motion Planning
-   RRT\*-Smart: Rapid convergence implementation of RRT\* towards optimal solution
-   Informed RRT\*: Optimal Sampling-based Path Planning Focused via Direct Sampling of an Admissible Ellipsoidal heuristic
-   Fast Marching Trees (FMT\*): a Fast Marching Sampling-Based Method for Optimal Motion Planning in Many Dimensions
-   Motion Planning using Lower Bounds (MPLB): Asymptotically-optimal Motion Planning using lower bounds on cost
-   Batch Informed Trees (BIT\*): Sampling-based Optimal Planning via the Heuristically Guided Search of Implicit Random Geometric Graphs
-   Advanced Batch Informed Trees (ABIT\*): Sampling-Based Planning with Advanced Graph-Search Techniques ((ICRA) 2020)
-   Adaptively Informed Trees (AIT\*): Fast Asymptotically Optimal Path Planning through Adaptive Heuristics ((ICRA) 2020)
