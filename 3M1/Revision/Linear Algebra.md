# Definition:
## Vector-space

## Matrices

## Norms
- Property:
	- $||x||>0, x \neq 0$
	- $||x||=0\text{ when x=0}$
	- $||kx||=|k|||x||$
	- $||x+y||\leq||x||+||y||$
- ln norm
	- $||x||_n =\left( \sum|x_{i}|^n \right)^{1/n}$
	- $||x||_{\infty}=max|x_{i}|$

- unit sphere and unit shell
	- unit ball (open)
	- unit ball (close)
	- unit shell
- Matrix norms
	- less intuitive than norms of vectors
	- expensive to compute
- operator norms
$$
||A||=\max_{x } \frac{||Ax||}{||x||}
$$
### Error Bounds

hello (to be filled)



# Interpolation
- issues with polynomial interpolation
	- ill-conditioned matrix
	- can be very sensitive to the choice of interpolation points
	- Runge effect
	- condition number increases when polynomial degree increased
- Orthogonal polynomials

- Orthogonal polynomials
$$
f = c_{n-1}x^{n-1}+c_{n-2}x^{n-2}+\dots+c_{1}x+c_{0}
$$
- Legendre polynomials
$$
(n+1)P_{n+1}(x)=(2n+1)xP_{n}(x)-nP_{n-1}(x)
$$
- $P_{0}=1, P_{1}=x$
- special features (orthogonal):
$$
\int_{-1}^{1}P_{m}(x)P_{n}(x)dx=0 \text{ if }m \neq n
$$

- Interpolation using Legendre polynomial


---

# Data Fitting
Minimising error in the $l_{2}$  norm, we've got the least square error:
$$
\min_{\hat{x} \in \mathbb{C}^n} ||r(\hat{x})|| = \min_{\hat{x} \in \mathbb{C}^n} ||A\hat{x} - b||
$$
Solving this and makeing the derivative to zero, we get:
$$

$$
