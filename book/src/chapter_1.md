# Chapter 1: Introduction & Roadmap

Welcome to the GA Physics Engine Workbook! This book is designed to be a practical, step-by-step companion for learning Geometric Algebra (GA) by applying it directly to physics simulation.

## Learning Path

We will build our intuition for GA not just by reading equations, but by understanding how they solve real-world problems in game physics. The roadmap is as follows:

1. **Chapter 2: Vectors, Bivectors, and Areas.** We'll learn the fundamental building blocks of GA. We'll write exercises to compute inner (dot) and outer (wedge) products, and visualize what they mean.
2. **Chapter 3: Rotors and 3D Rotation.** We'll replace matrices and quaternions with Rotors. You will practice creating rotors from bivectors and using them to rotate objects without gimbal lock.
3. **Chapter 4: Dynamics and Integration.** We'll tie it all together to create a rigid body simulator. You'll update position and orientation over time using GA derivatives.

## What You Need

To follow along with the exercises, you should be comfortable with:
- Basic vector math (what a vector is, addition, subtraction).
- Basic programming (Python or C++ is recommended, as the exercises will be presented conceptually in a Python-like pseudocode).

## Check Your Knowledge: Chapter 1

**Exercise 1.1: Why Geometric Algebra?**
In your own words, what is the primary advantage of learning Geometric Algebra for a physics engine compared to traditional vector math and quaternions?

> *Hint: Think about consistency across dimensions and the mathematical representation of "rotation".*

*(Self-check answer: GA provides a single unified mathematical framework for all dimensions. Instead of learning different rules for cross products (which only work in 3D) and quaternions (also 3D specific), GA uses rotors and the wedge product, which work consistently in 2D, 3D, and 4D. Rotors are also built directly from the plane of rotation, making them more intuitive.)*
