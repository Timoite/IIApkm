## Lecture 2: List of contents
- General algorithm
- Convergence criteria
- Rate of convergence
- Line search
- Interval reduction
- Golden section method
- Fitting with quadratic functions
- Fitting with a polynomial at three points
- Fitting with a polynomial at one point: Newton's method and quasi-Newton method


---

### Iterative Search Methods

1. Start with an initial guess, $x_0$, for the minimum of $f(x)$
2. Propose a __search direction__, $d_k$
3. Propose a step size $\alpha_k$ along $d_k$, typically, by an inner __line search__ loop to find the lowest value of $f(x)$ along the direction $d_k$
4. Update the estimate of the minimum location, $x_{k+1} = x_k+\alpha_k d_k$
5. Back to 2 until convergence

---

# Criteria

$$
||f(x_{k+1}) - f(x_{k}) || < \epsilon_{f}
$$
$$
||x_{k+1} - x_{k} || < \epsilon_{x}
$$
$$
||\nabla f(x_{k}) || < \epsilon_{g}
$$

---

### Rate of Convergence
The __rate of convergence__ of an algorithm quantifies how fast the approximate solution approaches the true minimum $x^*$, close to the minimum, iteration after iteration
$$

\lim_{k\rightarrow\infty} \frac{\left\| x_{k+1}-x^*\right\|}{\left\| x_k-x^* \right\|^p} = \beta

$$
The operation $\lim_{k\rightarrow\infty}$ means that the rate of convergence is an _asymptotic_ quantity.
- For the keen reader, the rate of convergence is the speed at which a sequence converges to its limit, if it converges
- $\beta$ is the __convergence ratio__: the smaller the better
- $p$ is the __order of convergence__.
	- $p=1$: linear convergence
	- $p=2$: quadratic convergence

---
#### Line Search
Interval reduction until the interval is smaller than a tolerance.
1. Start with three points, $x_1,x_2,x_3$ such that

$$f(x_1) \gt f(x_3)\;\;\;\textrm{and}\;\;\; f(x_3) \lt f(x_2)$$

$x_1$ and $x_2$ are the bounds, $x_3$ is the interior point
1. As a consequence of [Bolzano theorem](http://mathworld.wolfram.com/BolzanosTheorem.html), there exists a minimum in the interval $I_1 = [x_1,x_2]$.
This is called __bracketing__
1. Compute $f(x_4)$ at a fourth point $x_4 \in I_1$
2. If $f(x_4) \gt f(x_3)$, the minimum must be in $I_2 = [x_4,x_2]$, otherwise the minimum is in $I'_2=[x_1,x_3]$
3. Continue bracketing until the interval is smaller than a tolerance

#### Golden section search
- We impose a constant reduction factor $\beta$ for the interval length (convergence is linear, $p=1$)

$$\frac{I_2}{I_1} = \frac{\Delta x}{I_2} \text{ with }\Delta x = I_1 - I_2$$

set $\beta=I_2/I_1$, and solve quadratic:

  

$$\beta = \frac{\sqrt{5}-1}{2}\approx 0.618$$
It is optimal for binary search method...


#### Newton's Method

Fit a quadratic function by matching the function value, first and second derivative evaluated at a single point $x_{0}$:
$$
f(x) \approx g(x) = f(x_{0})+(x-x_{0})f^{'}(x_{0})+ \frac{1}{2}(x-x_{0})^2 f^{''}(x_{0})
$$
$$

x = x_0 - \frac{f'(x_0)}{f''(x_0)}

$$

#### Quasi-Newton Method

$$

x = x_1 - f'(x_1) \frac{x_1-x_0}{f'(x_1)-f'(x_0)}

$$



