Optimization is the process of finding the best solution from all feasible solutions. It involves maximizing or minimizing an objective function subject to constraints.

Quantity to be minimized or maximized is called:
1. objective function
2. cost function
3. utility function
4. loss function

Parameters to be changed are called:
1. control variables
2. decision variables

Restriction on the allowed parameters are called constraints.


Mathematically, the problem is to minimize $f(x)$ subject to:
1. Equality:
$$
c_{i}(x) = 0, i=1, \dots, m^{'}
$$
2.  Inequality:
$$
c_{i}(x) = 0, i=m^{'}+1, \dots, m
$$

When minimizing $f(x) subject to constraints, $S$ is the feasible region and any $x \in S$ is a feasible solution. For unconstrained problem, $S$ is infinitely large.

__Gradient__:
$$

g(x) = \nabla f(x) = \left[\frac{\partial f}{\partial x_1},\frac{\partial f}{\partial x_2},\ldots,

\frac{\partial f}{\partial x_N}\right]^T

$$

__[[Hessian]]__:
$$

H(x) = \nabla(\nabla f(x)) =

\begin{bmatrix}

\frac{\partial^2 f}{\partial x_1^2} & \ldots & \frac{\partial^2 f}{\partial x_1 \partial x_N}\\

\vdots & \ddots & \vdots\\

\frac{\partial^2 f}{\partial x_N \partial x_1} & \ldots & \frac{\partial^2 f}{\partial x_N^2}

\end{bmatrix}

$$
Hessian is a symmetric matrix by definition

### Feasible direction

At a feasible point $x$, a direction $d$ is a __feasible direction__ if an arbitrary small move from $x$ in direction $d$ remains feasible.

![[Pasted image 20250311150303.png]]


## Types of minima

![[Pasted image 20250311150948.png]]

---

### Unimodality

A function is __unimodal__ if it has only one extremum

It is __strongly unimodal__ if along a straight line from every point to the extremum the gradient is negative (for a minimum) or positive (for a maximum)


---

### Convex function

- A function is convex if its graph at any point $y$ is never below the tangent at any other point $x$

- Mathematically

$$ f(y) \ge f(x) + \nabla f(x)^T (y-x)$$

- It is strictly convex if instead of $\ge$ we use $>$

- Convex functions have a _global_ minimum

- Convex functions are unimodal, but not all unimodal functions are convex

This is a counter example: negative gaussian

![[Pasted image 20250311151826.png]]

---

### Necessary condition for local minimum
A __necessary__ condition for $x^*$ to be a _local minimum_ of $f(x)$ in $S$ is
$$

\nabla f(x^*) \cdot d \ge 0

$$
for all _feasible direction_ d.

If $x^*$ is an __interior point__, i.e., it is not at the boundary of the feasible region:
- because all directions are feasible, $x^*$ must be a stationary point when $$\nabla f(x^*) = 0$$
- The condition $\nabla f(x^*) = 0$ is __necessary but not sufficient__ for $x^*$ to be a minimum, because it can also be a _saddle point_. 


#### Univariate

For the _univariate_ case (i.e., $x\in\mathbb{R})$, the __Taylor expansion__ around $x^*$ is

$$\boxed{\large f''(x^*) \gt 0}\strut$$

- At a stationary point $x^*$, $f''(x^*)>0$ is a sufficient condition of strong local minimum
- At a stationary point, $f''(x^*)\ge0$ is a necessary condition of strong local minimum (it is necessary that $f''(x^*)$ be non-negative. If it is negative, $x^*$ cannot be a minimum.)
- If $f''(x^*)=0$, we need to analyse the higher order terms

#### Multivariate

$$

\boxed{\large d^T H(x^*) d > 0 \qquad \forall d\strut}

$$

- At a stationary point $x^*$, $\large d^T H(x^*) d > 0$ (the Hessian is __positive definite__) is a [[Necessary Condition & Sufficient Condition|Sufficient Condition]] of strong local minimum.

- At a stationary point $x^*$, $\large d^T H(x^*) d \ge 0$ (the Hessian is __positive semidefinite__) is a necessary condition of strong local minimum.


If $H(x)$ is [[positive definite]] everywhere (e.g. for a quadratic function), $f$ is a __convex function__, and therefore the minimum is unique and a _global minimum_.

---
