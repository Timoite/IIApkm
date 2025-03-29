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
Solving this and making the derivative to zero, we get:
$$
\hat{x} = (A^H A)^{-1} A^H b \\
= A^+ b
$$
---

# Iterative methods for linear systems
Direct methods can be expensive when the matrix is large. It does not scale well and is sequential, not suitable for parallel computers.

for iterative solvers:
- less complexity
- less memory
- some can solve singular problems
- can be terminated early
- are often suited to large, parallel computer

## An iterative method for the largest eigenvalue and eigenvector
recall that a vector x can be expressed in terms of the n eigenvectors of a $n \times n$ matrix, if we multiple x repeatedly by A:
$$
\underbrace{AA \dots A}_{k \text{ times}} x = A^k x = \sum_{i=1}^{n} \alpha_i \lambda_i^k u_i,
$$
### Rayleigh quotient
To find an estimate of eigenvalue, we pose a minimisation problem:
$$
\min_{\lambda^* \in \mathbb{C}} ||Ax - \lambda^* x||_2.
$$

Hence:

$$
\lambda^* = R(A, x) = \frac{x^H A x}{x^H x},
$$

where R is known as the Rayleigh quotient.

## Stationary method for Ax = b
$A = N - P$, $Nx = b +Px$, so:
$$
Nx_{k+1} = b + Px_k,
$$

is a way to approximate a solution.
Three classic examples:
- Richardson iteration
- Jacobi method
- Gauss-Seidel

#### Convergence
Defining the error at the kth iterate:
$$
e_{k} = x_{exact}-x_{k}
$$
therefore:
$$
e_{k+1}=N^{-1}Pe_{k}
$$
$$
e_{k}=(N^{-1}P)^ke_{0}=c_{1}\lambda_{1}^ku_{1}\dots
$$
will converge if 
$$
\rho(N^{-1}P)<1
$$
where $\rho$ is the largest absolute eigenvalue of the matrix, which is also called spectral radius

### Conjugate gradient method
as a direct method:
consider we have a set P of n non-zero vectors that are A-conjugate, where A-conjugrate implied that:
$$
p_{i}^HAp_{j}=0 \text{ if } i \neq j
$$

$$
Ax = \sum_{i=0}^{n-1} \alpha_i Ap_i = b.
$$

$$
p_j^H Ax = \sum_{i=0}^{n-1} \alpha_i p_j^H Ap_i = \alpha_j p_j^H Ap_j = p_j^H b
$$
$$
\alpha_j = \frac{p_j^H b}{p_j^H A p_j}
$$

Note that the CG method is monotone in the A-norm, and the rate of convergence is affected by he condition number:
$$
\frac{||e_k||_A}{||e_0||_A} \leq 2 \left( \frac{\sqrt{\kappa_2} - 1}{\sqrt{\kappa_2} + 1} \right)^k
$$

#### Preconditioning
to enhance the convergence rate, we can use preconditioning:
$$
P^{-1}Ax = P^{-1}b
$$
where $P^{-1}$ must be cheap to apply for efficiency but close enough to $a^{-1}$  to be effective.

---

# Singular value decomposition (SVD)

## Definition and properties

### matrix Diagonalisation
For Hermitian matrix M:
$$
Q^H M Q = \Lambda
$$
the columns of Q are the $l_{2}$ normalised eigenvectors of M. Q is a unitary matrix since the eigenvectors of M is orthogonal.

#### Multiplication of a diagonal matrix
$$
AD = \begin{bmatrix} d_1 a_1 & \dots & d_n a_n \end{bmatrix}
$$





