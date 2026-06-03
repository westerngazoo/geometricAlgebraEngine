# API Reference

This page outlines the core classes and functions intended for the GA Physics Engine. *(Note: This is a design document, actual implementation details may vary depending on the language used).*

## `Multivector`

The fundamental algebraic class.

- `Multivector(scalar, e1, e2, e3, e12, e23, e31, e123)`: Constructor for a general 3D multivector.
- `add(other)`: Returns the sum of two multivectors.
- `sub(other)`: Returns the difference.
- `mul(other)`: The Geometric Product. Returns $A B$.
- `wedge(other)`: The Outer Product. Returns $A \wedge B$.
- `dot(other)`: The Inner Product. Returns $A \cdot B$.
- `reverse()`: Reverses the order of blades in the multivector.
- `grade(n)`: Extracts only the components of grade $n$.

## `Rotor`

A subclass or specialized type of Multivector representing rotations.

- `Rotor(angle, bivector_plane)`: Constructs a rotor that rotates by `angle` in the `bivector_plane`.
- `rotate(vector)`: Applies the rotation to a vector: $R v \tilde{R}$.
- `normalize()`: Ensures the rotor maintains unit magnitude to prevent numerical drift.

## `RigidBody`

Represents a physical object in the simulation.

- `position`: Vector (Grade 1).
- `linear_velocity`: Vector (Grade 1).
- `mass`: Scalar (Grade 0).
- `orientation`: Rotor (Even grades).
- `angular_velocity`: Bivector (Grade 2).
- `inertia`: Function or representation that maps Bivector to Bivector.

### Methods

- `apply_force(force_vector, point_vector)`: Applies a linear force at a specific point, automatically calculating torque as `(point_vector - position) ^ force_vector`.
- `update(dt)`: Integrates linear and angular equations of motion over timestep `dt`.

## `World`

Manages the simulation environment.

- `add_body(body)`: Registers a `RigidBody`.
- `step(dt)`: Advances the simulation by applying forces, checking collisions, and calling `update(dt)` on all bodies.
