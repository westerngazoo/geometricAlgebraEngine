# Chapter 2: Vectors, Bivectors, and Areas

In this chapter, we explore the core elements of GA: **Blades**.

## The Wedge Product

The wedge product (outer product), denoted by $\wedge$, is the operation that creates higher-grade blades from lower-grade ones.

When you wedge two vectors $u$ and $v$:
$$B = u \wedge v$$
The result $B$ is a **bivector**. A bivector represents an oriented area segment. It has magnitude (the area of the parallelogram formed by $u$ and $v$) and an orientation (the plane it lies in).

### Key Properties of the Wedge Product:

1. **Anti-symmetry:** $u \wedge v = -(v \wedge u)$. Reversing the order flips the orientation.
2. **Parallel Vectors:** If $u$ and $v$ are parallel, $u \wedge v = 0$.

## The Geometric Product

The geometric product $uv$ of two vectors combines the dot product (scalar) and the wedge product (bivector):

$$uv = u \cdot v + u \wedge v$$

## Exercises: Chapter 2

Assume an orthonormal basis $e_1, e_2, e_3$ (corresponding to X, Y, Z axes).
Remember that $e_1 \wedge e_2$ is often written as $e_{12}$.
Also remember that basis vectors square to 1: $e_1 e_1 = 1$, and orthogonal basis vectors anti-commute: $e_1 e_2 = -e_2 e_1 = e_{12}$.

**Exercise 2.1: Calculating a Wedge Product**
Given $u = 2e_1 + e_2$ and $v = 3e_1 + 4e_2$, calculate the bivector $u \wedge v$.

> *Step-by-step:*
> 1. Substitute the vectors: $(2e_1 + e_2) \wedge (3e_1 + 4e_2)$
> 2. Expand using the distributive property:
>    $= 6(e_1 \wedge e_1) + 8(e_1 \wedge e_2) + 3(e_2 \wedge e_1) + 4(e_2 \wedge e_2)$
> 3. Apply properties (wedge of a vector with itself is 0, anti-symmetry):
>    $= 0 + 8e_{12} - 3e_{12} + 0$
> 4. Simplify.

*(Self-check answer: $5e_{12}$. This represents an area of 5 lying in the XY plane.)*

**Exercise 2.2: Geometric Product Calculation**
Calculate the geometric product of $e_1$ and $(e_1 + e_2)$.

> *Step-by-step:*
> 1. Expand: $e_1(e_1 + e_2) = e_1e_1 + e_1e_2$
> 2. Use basis properties ($e_1e_1 = 1$, $e_1e_2 = e_{12}$).

*(Self-check answer: $1 + e_{12}$. Notice the result is a Multivector containing a scalar (Grade 0) and a bivector (Grade 2).)*
