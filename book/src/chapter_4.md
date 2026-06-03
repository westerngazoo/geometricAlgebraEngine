# Chapter 4: Dynamics and Integration

Now we apply what we've learned to simulate rigid body motion over time.

## Linear vs Angular

| Concept | Linear (Vectors) | Angular (Bivectors/Rotors) |
| :--- | :--- | :--- |
| **State** | Position ($x$) | Orientation ($R$) |
| **Velocity** | Linear Vel ($v$) | Angular Vel ($B$) |
| **Mass/Inertia**| Mass ($m$) | Inertia Map ($I(B)$) |
| **Force/Torque**| Force ($F$) | Torque ($\tau = r \wedge F$) |

## Integrating the Rotor

To move an object forward in time ($\Delta t$), we update its position and velocity.

$$x_{new} = x_{old} + v \Delta t$$
$$v_{new} = v_{old} + (F/m) \Delta t$$

For orientation, the derivative of a rotor $R$ with respect to time, given an angular velocity bivector $B$, is:

$$\frac{dR}{dt} = -\frac{1}{2} B R$$

So, a simple Euler integration step for orientation is:

$$R_{new} = R_{old} - \frac{1}{2} (B R_{old}) \Delta t$$

After integration, numerical errors will cause $R_{new}$ to drift away from being a perfect rotor (its magnitude won't be exactly 1). We must **normalize** it: $R_{new} = R_{new} / |R_{new}|$.

## Exercises: Chapter 4

**Exercise 4.1: Calculating Torque**
A force $F = 10e_2$ (10 Newtons in the Y direction) is applied to an object at a position $r = 2e_1$ relative to its center of mass.
Calculate the torque bivector $\tau = r \wedge F$.

*(Self-check answer: $\tau = (2e_1) \wedge (10e_2) = 20(e_1 \wedge e_2) = 20e_{12}$. The torque is trying to spin the object in the XY plane with a magnitude of 20.)*

**Exercise 4.2: Code Structure (Pseudocode)**
Write a simple `update(dt)` function in pseudocode for a `RigidBody` class using GA concepts.

> *Hint: Update linear velocity, linear position, angular velocity (ignoring inertia for simplicity, assume $\Delta B = \tau \Delta t$), and finally orientation.*

*(Self-check answer:*
```python
def update(self, dt):
    # Linear
    self.linear_velocity += (self.force / self.mass) * dt
    self.position += self.linear_velocity * dt

    # Angular
    # (Assuming self.torque is already accumulated as a bivector)
    # Note: proper physics requires the inertia tensor here: B_new = B_old + I_inv(torque) * dt
    self.angular_velocity += self.torque * dt

    # Update Rotor
    rotor_derivative = -0.5 * (self.angular_velocity * self.orientation)
    self.orientation += rotor_derivative * dt
    self.orientation.normalize()

    # Reset forces/torques for next frame
    self.force = Vector(0)
    self.torque = Bivector(0)
```
*)*
