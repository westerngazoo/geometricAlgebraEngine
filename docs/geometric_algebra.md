# Geometric Algebra Concepts

This physics engine uses Geometric Algebra (GA) instead of traditional linear algebra (vectors and cross products) or quaternions. This page introduces the fundamental mathematical concepts.

## What is Geometric Algebra?

Geometric Algebra is an extension of linear algebra that naturally unifies operations on scalars, vectors, areas, and volumes. Instead of needing different mathematical tools for different dimensions or types of geometry (like needing quaternions for 3D rotation, complex numbers for 2D rotation, and vectors for translation), GA provides a single unified framework.

## Core Elements: Blades and Multivectors

In GA, we work with elements called **blades**, which represent geometric entities of varying dimensions:

- **Grade 0 (Scalars):** Simple numbers (e.g., mass, time).
- **Grade 1 (Vectors):** Directed line segments (e.g., position, velocity).
- **Grade 2 (Bivectors):** Directed plane segments. Think of them as areas with an orientation (clockwise or counter-clockwise). They naturally represent torque, angular momentum, and rotation.
- **Grade 3 (Trivectors / Pseudoscalars):** Directed volumes.

A **Multivector** is a linear combination of blades of different grades. It is the fundamental object in GA, analogous to a complex number having both a real and imaginary part.

## The Geometric Product

The defining operation of GA is the **Geometric Product** of two vectors, denoted as $uv$. It is defined as the sum of the inner (dot) product and the outer (wedge) product:

$$uv = u \cdot v + u \wedge v$$

- $u \cdot v$ (Inner Product): A scalar (Grade 0), capturing how parallel the vectors are.
- $u \wedge v$ (Wedge Product): A bivector (Grade 2), capturing how perpendicular the vectors are. It represents the oriented area spanned by $u$ and $v$.

## Rotors: The GA Way to Rotate

In 3D, traditional physics engines use Quaternions or Euler angles for rotation. GA uses **Rotors**.

A Rotor $R$ is a multivector that contains only even grades (a scalar and a bivector). It elegantly encodes rotation in any number of dimensions.

To rotate a vector $v$ using a rotor $R$, we compute:

$$v' = R v \tilde{R}$$

Where $\tilde{R}$ is the "reverse" of the rotor (similar to a quaternion conjugate).

### Why use Rotors instead of Quaternions?

- **Generality:** Rotors work in 2D, 3D, 4D, and beyond without changing the underlying mathematical structure.
- **Geometric Intuition:** A rotor is directly constructed from the plane of rotation (a bivector) and the angle, making it much more intuitive to understand geometrically than a quaternion.
- **No Gimbal Lock:** Like quaternions, rotors do not suffer from gimbal lock.

## Summary

By understanding vectors (lines), bivectors (areas), and rotors (rotations), you are equipped to understand the physics simulation engine that runs on these principles.
