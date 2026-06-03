# Physics Engine Architecture

This document describes how traditional physics concepts are mapped to Geometric Algebra (GA) in this engine.

## Rigid Body Dynamics

A standard rigid body requires tracking position, linear velocity, orientation, and angular velocity.

### Linear Kinematics

Linear concepts translate directly to GA Vectors (Grade 1):

- **Position ($x$):** Represented as a vector.
- **Velocity ($v$):** Represented as a vector.
- **Force ($F$):** Represented as a vector.
- **Linear Momentum ($p$):** Represented as a vector ($p = m v$).

The update rule remains standard numerical integration (e.g., Euler or Verlet):

$$v_{new} = v_{old} + (F / m) \Delta t$$
$$x_{new} = x_{old} + v_{new} \Delta t$$

### Angular Kinematics

This is where GA shines. Instead of using pseudo-vectors (cross products) which behave inconsistently under reflections and require right-hand rules, we use Bivectors.

- **Orientation ($R$):** Represented as a Rotor (Scalar + Bivector).
- **Angular Velocity ($B$):** Represented as a Bivector (Grade 2). It directly encodes the plane of rotation and the magnitude of the velocity.
- **Torque ($\tau$):** Represented as a Bivector. It is the exterior product (wedge product) of the moment arm and force: $\tau = r \wedge F$.
- **Angular Momentum ($L$):** Represented as a Bivector.

#### Updating Orientation

To update the orientation Rotor $R$ given an angular velocity bivector $B$ over a timestep $\Delta t$, we use the rotor derivative:

$$\frac{dR}{dt} = -\frac{1}{2} B R$$

So the numerical update is:

$$R_{new} = R_{old} - \frac{1}{2} (B R_{old}) \Delta t$$

*(Note: In practice, the resulting rotor must be normalized after integration to prevent drift).*

## Collision Detection

Collision detection often relies on geometric primitives. GA provides elegant ways to represent and intersect geometry using conformal or projective models, but for a basic engine, we can still use standard vector math mixed with GA concepts.

- **Points:** Vectors.
- **Planes:** Can be represented as vectors (normal) combined with a scalar distance, or naturally as Duals of Vectors in GA.
- **Intersection Tests:** The wedge product can be used to determine if points are coplanar or to calculate volumes (using trivectors) to check for overlap.

## Inertia Tensor

In standard 3D physics, inertia is a $3 \times 3$ matrix. In GA, inertia is a linear function that maps a Bivector (angular velocity) to another Bivector (angular momentum):

$$L = I(B)$$

This mapping is symmetric and can be implemented without needing to drop into matrix representations, keeping the mathematical framework purely geometric.
