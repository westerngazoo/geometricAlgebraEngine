# Chapter 3: Rotors and 3D Rotation

Rotations in GA are handled by **Rotors**. A rotor $R$ is a multivector composed of a scalar and a bivector. It is analogous to a quaternion but derived geometrically.

## Constructing a Rotor

To rotate by an angle $\theta$ in a plane defined by a unit bivector $B$, the rotor is defined using Euler's formula for GA:

$$R = \exp(-B \theta / 2) = \cos(\theta / 2) - B \sin(\theta / 2)$$

Notice the half-angle! This is because to rotate a vector $v$, we apply the rotor from both sides:

$$v' = R v \tilde{R}$$

Where $\tilde{R}$ is the reverse of the rotor: $\tilde{R} = \cos(\theta / 2) + B \sin(\theta / 2)$.

## The Power of Bivectors for Rotation

In traditional physics engines, you define rotation using a rotation axis (a vector). In GA, you define rotation using the plane of rotation (a bivector). This is much more intuitive: to spin something around the Z-axis, you are actually spinning it *within* the XY plane ($e_{12}$).

## Exercises: Chapter 3

**Exercise 3.1: Creating a Rotor**
Construct the rotor $R$ that rotates a vector by $90^\circ$ ($\pi/2$ radians) in the XY plane ($e_{12}$). Let $\theta = \pi/2$, so $\theta/2 = \pi/4$.
Assume the basis bivector $e_{12}$ is our unit bivector $B$.

> *Step-by-step:*
> 1. Use the formula: $R = \cos(\pi/4) - e_{12} \sin(\pi/4)$
> 2. Evaluate sine and cosine: $\cos(\pi/4) = \sqrt{2}/2$, $\sin(\pi/4) = \sqrt{2}/2$.

*(Self-check answer: $R = \frac{\sqrt{2}}{2} - \frac{\sqrt{2}}{2} e_{12}$.)*

**Exercise 3.2: Applying the Rotor**
Using the rotor $R$ from Exercise 3.1, rotate the vector $v = e_1$ (a unit vector pointing along the X axis).
Compute $v' = R e_1 \tilde{R}$.

> *Hint:*
> - $R = \frac{\sqrt{2}}{2}(1 - e_{12})$
> - $\tilde{R} = \frac{\sqrt{2}}{2}(1 + e_{12})$
> - Remember that $e_{12} e_1 = e_1 e_2 e_1 = -e_1 e_1 e_2 = -e_2$.
> - Multiply carefully: $v' = \frac{1}{2} (1 - e_{12}) e_1 (1 + e_{12})$

*(Self-check answer: Let's do the math.
First, $R e_1 = \frac{\sqrt{2}}{2}(e_1 - e_{12}e_1) = \frac{\sqrt{2}}{2}(e_1 - (-e_2)) = \frac{\sqrt{2}}{2}(e_1 + e_2)$.
Next, multiply by $\tilde{R}$:
$v' = \frac{\sqrt{2}}{2}(e_1 + e_2) \frac{\sqrt{2}}{2}(1 + e_{12}) = \frac{1}{2} (e_1 + e_1 e_{12} + e_2 + e_2 e_{12})$.
We know $e_1 e_{12} = e_1 e_1 e_2 = e_2$.
We know $e_2 e_{12} = e_2 e_1 e_2 = -e_1 e_2 e_2 = -e_1$.
So, $v' = \frac{1}{2} (e_1 + e_2 + e_2 - e_1) = \frac{1}{2} (2e_2) = e_2$.
Rotating the X-axis vector ($e_1$) by $90^\circ$ in the XY plane results in the Y-axis vector ($e_2$). The math works!)*
