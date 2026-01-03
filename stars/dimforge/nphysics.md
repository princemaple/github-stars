---
project: nphysics
stars: 1644
description: 2 and 3-dimensional rigid body physics engine for Rust.
url: https://github.com/dimforge/nphysics
---

**Users guide | 2D Documentation | 3D Documentation | Forum**

⚠️\*\*This crate is now passively-maintained. It is being superseded by the Rapier project.\*\*⚠️

* * *

nphysics
========

**nphysics** is a 2 and 3-dimensional physics engine for games and animations. It uses ncollide for collision detection, and nalgebra for vector/matrix math. 2D and 3D implementations both share the same code!

Examples are available in the `examples2d` and `examples3d` directories. Interactive 3D are available there. Because those demos are based on WASM and WebGl 1.0 they should work on most modern browsers. Feel free to ask for help and discuss features on the official user forum.

Why another physics engine?
---------------------------

There are a lot of physics engine out there. However having a physics engine written in Rust is much more fun than writing bindings and has several advantages:

-   It shows that Rust is suitable for soft real-time applications. − It features an efficient implementation of multibodies using the reduced-coordinates approach. Constraint-based joints are also supported.
-   It shows that there is no need to write two separate engines for 2D and 3D: genericity wrt the dimension is possible (modulo low level arithmetic specializations for each dimension).
-   In a not-that-near future, C++ will die of ugliness. Then, people will search for a physics engine and **nphysics** will be there, proudly exhibiting its _Rusty_ sexiness.

Features
--------

-   Static, dynamic, and kinematic rigid bodies.
-   Common convex primitives: box, ball, convex polyhedron.
-   Concave geometries built from convex primitives: compound geometries, triangle mesh, polylines.
-   Multibodies using reduced-coordinates approaches or constraints-based joints.
-   Multibody joint limits and motors.
-   Stable stacking due to non-linear a position-based penetration correction and one-shot contact manifold generation.
-   Island based sleeping (objects deactivation when they are at rest).
-   Ray casting.
-   Swept sphere based continuous collision detection.
-   Ball-in-socket joint.
-   FixedJoint joint.
-   Sensors.
-   Deformable bodies (aka. soft-bodies)
-   Kinematic bodies
-   WASM support

What is missing?
----------------

**nphysics** is a very young library and needs to learn a lot of things to become a grown up. Many missing features are because of missing features on **ncollide**. Features missing from **nphysics** itself include:

-   more joints, joint limits, joint motors and breakable joints.
-   parallel pipeline
-   GPU-based pipeline

Dependencies
------------

The libraries needed to compile the physics engine are:

-   ncollide: the collision detection library.
-   nalgebra: the linear algebra library.

The libraries needed to compile the examples are:

-   kiss3d: the 3d graphics engine.
