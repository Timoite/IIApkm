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
$$
M = Q \Lambda Q^H.
$$

the columns of Q are the $l_{2}$ normalised eigenvectors of M. Q is a unitary matrix since the eigenvectors of M is orthogonal.

#### Multiplication of a diagonal matrix
$$
AD = \begin{bmatrix} d_1 a_1 & \dots & d_n a_n \end{bmatrix}
$$
$$
M = \sum_i \lambda_i u_i u_i^H
$$

note that all Hermitian matrices can be diagonalised, and has sign ambiguity.

#### Definition of SVD
$$
A = U \Sigma V^H
$$
what should they be?

pre-multiplied by $A^H$:
$$
\begin{aligned}
A^H A &= (U \Sigma V^H)^H U \Sigma V^H \\
&= V \Sigma^H U^H U \Sigma V^H \\
&= V \Sigma^H \Sigma V^H.
\end{aligned}
$$
- $A^H A$ is Hermitian
- $\Sigma^H \Sigma$ is diagonal with entries $\sigma_{1}^2\dots \sigma_{p}^2$
- so it is the diagonalisation of the square matrix $A^H A$ 
	- Columns of V are the normalised eigenvectors of $A^H A$ 
	- The diagonal entries of  $\Sigma^H \Sigma$  are the eigenvalues of $A^H A$ 

if post-multiplying:
$$
A = U \Sigma V^H \text{ by } V,
$$
$$
AV = U \Sigma
$$
$$
Av_i = \sigma_i u_i
$$

---
### Reduced SVD
![[Pasted image 20250329170355.png]]

---
### Computing the SVD
See lecture notes, general steps:
1. compute eigenvalues/vectors of $AA^T$ to get $U$ and $\Sigma$
2. compute eigenvalues/vectors of $A^TA$ to get $V$
3. reduce the SVD

---

### low-rank approximation
similar to principal axis? reduce the rank of A to k.
$$
A_k = \sum_{i=1}^k \sigma_i u_i v_i^H
$$

optimality:

$$
\begin{aligned}
A - A_k &= \sum_{i=1}^r \sigma_i u_i v_i^H - \sum_{i=1}^k \sigma_i u_i v_i^H \\
&= \sum_{i=k+1}^r \sigma_i u_i v_i^H
\end{aligned}
$$

$$
\begin{aligned}
\|A - A_k\|_2 &= \left\| \sum_{i=k+1}^r \sigma_i u_i v_i^H \right\|_2 \\
&= \sigma_{k+1}
\end{aligned}
$$

---

### Application of SVD



---

### The effective rank
The effective rank is the number of singular values that are greater than the noise level

### Least-squares solutions
$$
\hat{x} = (A^H A)^{-1} A^H b = A^+ b,
$$

In full rank, we decompose:
$$
A = \begin{bmatrix} U_1 & U_2 \end{bmatrix} \begin{bmatrix} \Sigma_1 \\ 0 \end{bmatrix} V^H.
$$
least square minimise:
$$
\begin{aligned}
r = \|A \hat{x} - b\|_2^2 &= \left\| \begin{bmatrix} U_1^H \\ U_2^H \end{bmatrix} (A \hat{x} - b) \right\|_2^2 \\
&= \left\| \begin{bmatrix} U_1^H \\ U_2^H \end{bmatrix} (U_1 \Sigma_1 V^H \hat{x} - b) \right\|_2^2 \\
&= \left\| \begin{bmatrix} \Sigma_1 V^H \hat{x} - U_1^H b \\ -U_2^H b \end{bmatrix} \right\|_2^2 \\
&= \|\Sigma_1 V^H \hat{x} - U_1^H b\|_2^2 + \|U_2^H b\|_2^2.
\end{aligned}
$$

which is minimised when $$
\Sigma_1 V^H x = U_1^H b,
$$
so $$
\hat{x} = V \Sigma_1^{-1} U_1^H b.
$$
where 
$$
\Sigma^+ = \begin{bmatrix}
1/\sigma_1 & & \\
& \ddots & \\
& & 1/\sigma_n
\end{bmatrix}
$$

---

### Stability
if the smallest singular value $\sigma_{min}$ is small, then the least squares solution will be large and very sensitive to changes in b.

this is the case for full rank. if $\sigma_{min}=0$, we cannot compute a unique least squares solutions.


---
# PCA

### Covariance matrix
$$
\mathbb{E} \begin{pmatrix} \begin{bmatrix} (X_1 - \mu_1)^2 & (X_1 - \mu_1)(X_2 - \mu_2) & (X_1 - \mu_1)(X_3 - \mu_3) \\ (X_2 - \mu_2)(X_1 - \mu_1) & (X_2 - \mu_2)^2 & (X_2 - \mu_2)(X_3 - \mu_3) \\ (X_3 - \mu_3)(X_1 - \mu_1) & (X_3 - \mu_3)(X_2 - \mu_2) & (X_3 - \mu_3)^2 \end{bmatrix} \end{pmatrix}
$$


### Sample data
$$
X = \begin{bmatrix}
\uparrow & \uparrow & & \uparrow \\
x_1 & x_2 & \dots & x_p \\
\downarrow & \downarrow & & \downarrow
\end{bmatrix}
$$


### Sample mean
$$
\bar{x}_j := \frac{1}{n} \sum_{i=1}^{n} X_{ij},
$$

In matrix notation:
$$
\bar{x} = \frac{1}{n} X^T 1_n,
$$


### sample covariance matrix
$$
\begin{aligned}
S &= \frac{1}{n-1}(X - 1_n \bar{x}^T)^T (X - 1_n \bar{x}^T) \\
&= \frac{1}{n-1}(X - \frac{1}{n} 1_{n \times n} X)^T (X - \frac{1}{n} 1_{n \times n} X)
\end{aligned}
$$










