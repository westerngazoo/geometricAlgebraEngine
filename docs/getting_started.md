# Getting Started

This guide will walk you through setting up a basic scene in the GA Physics Engine.

## 1. Initialization

First, create a simulation world.

```python
# Conceptual example
from ga_physics import World, RigidBody, Vector, Bivector, Rotor

world = World()
world.gravity = Vector(0, -9.81, 0)
```

## 2. Creating an Object

Let's create a simple box. We need to define its mass, initial position, and initial orientation.

```python
box = RigidBody(mass=10.0)
box.position = Vector(0, 10, 0) # Start 10 units in the air
```

## 3. Applying Rotation using GA

Instead of Euler angles, we give the box an initial angular velocity using a **Bivector**. A bivector defines the plane of rotation.

Let's make it spin in the XY plane. The basis vectors are $e_1$ (X) and $e_2$ (Y). The bivector for the XY plane is $e_1 \wedge e_2$ (often written as $e_{12}$).

```python
# Spin at 2 radians per second in the XY plane
box.angular_velocity = Bivector(e12=2.0)
```

## 4. Applying Forces

You can apply forces to the object. The engine will automatically use the wedge product to calculate the resulting torque.

```python
# Apply an impulse force off-center
force = Vector(50, 0, 0)
point_of_application = Vector(0, 10.5, 0) # Slightly above the center of mass

box.apply_force(force, point_of_application)
world.add_body(box)
```

## 5. Running the Simulation

Finally, run the simulation loop. The `world.step()` function will handle the geometric integration of both the linear vectors and the orientation rotors.

```python
dt = 1.0 / 60.0 # 60 Hz

for frame in range(600):
    world.step(dt)
    print(f"Frame {frame}: Position={box.position}, Orientation={box.orientation}")
```

Notice how we didn't need any cross products or quaternions! The rotation was defined entirely by the bivector plane, and the integration handles the rotor updates naturally.
