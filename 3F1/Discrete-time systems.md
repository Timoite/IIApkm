# Discrete time signals
Discrete time signals can be classified as 
- right-sided ($s = (s_m, s_{m+1}, s_{m+2},...)$), 
- left-sided ($s_k = 0$ for $k > m$), two-sided, 
- or finite-length ($s = (s_m, s_{m+1},..., s_{m+l-1})$). 
This course will focus mainly on right-sided signals. 

A **right-sided signal** starting at zero ($s = \{s_k\}_{k\geq0} = s_0, s_1, s_2,...$) is also called a **semi-infinite sequence**.


# Normalised sampling
A discrete time signal or semi-infinite sequence $\{x_k\}_{k\geq0}$ could be a sampled continuous signal, where $s_k = s(kT)$, $T$ is the sampling interval. 

When discussing a normalised frequency $\theta$, the true frequency can always be recovered as $$f=\frac{\theta}{2\pi} f_{s}$$
nice way to remember:
$$
2\pi\frac{ f}{f_{s}}=\theta
$$
Signal processing techniques are independent of unit or sampling interval. 

**Normalised time/frequency: $T = 1$ second, sampling frequency $f_s = 1$ Hertz, or $\theta_s = 2\pi$ radians per second.**


# Discrete Time System

The definition of a Linear Time-Invariant (LTI) system $L$ extends naturally from continuous to discrete time; it is 
- linear if $L(\alpha_1 u_k + \alpha_2 u'_k) = \alpha_1 y_k + \alpha_2 y'_k$ and 
- time-invariant if $L(u_{k+m}) = y_{k+m}$ for any $m$, 
- with discrete LTI systems governed by linear difference equations such as $y_k + \alpha y_{k-1} + \beta y_{k-2} = u_k$.


# Kronecker Delta signal and response
The Kronecker delta signal, denoted as ${\delta_k}$, is defined as 1 when $k = 0$ and 0 otherwise, and $\delta_k = 0$ for $k < 0$. 

Any input signal ${u_k}$ to a Linear Time-Invariant System (LTIS) can be expressed as $u_k = \sum_{n=-\infty}^{\infty} \delta_n u_{k-n}$ for every $k$. 

The output signal ${y_k}$ satisfies $y_k = \sum_{n=-\infty}^{\infty} g_n u_{k-n}$ for every $k$, where ${g_k}$ represents the **delta response of the LTIS**, and is equivalent to the difference equation in defining/describing the LTIS.


# Discrete convolution
Discrete convolution is defined by the equation $y_k = \sum_{n=-\infty}^{\infty} g_n u_{k-n}$ for all $k$, and 
- is denoted as $y = g * u$. 
- It is analogous to continuous convolution, $y(t) = \int_{-\infty}^{\infty} g(\tau)u(t - \tau)d\tau$,
- and is commutative: $\sum_{n=-\infty}^{\infty} g_n u_{k-n} = \sum_{n=-\infty}^{\infty} g_{k-n} u_n$.


## Special Cases
For semi-infinite sequences $y = \{g_k\}_{k \geq 0} * \{u_k\}_{k \geq 0}$, the discrete convolution simplifies to $$y_k = \sum_{n=0}^{k} g_n u_{k-n}$$, because $g_n = 0$ for $n < 0$ and $u_{k-n} = 0$ for $n > k$. 

For a finite sequence $g$, where $g_k = 0$ for $k > l$, the convolution becomes $$y_k = \sum_{n=0}^{\min(l,k)} g_n u_{k-n}$$. These special cases arise due to the properties of the sequences involved, and the original definition with a sum from $-\infty$ to $\infty$ remains valid in all cases.


# Properties of the Delta response
The delta response is also known as "pulse response" or "impulse response". 

A Finite Impulse Response (FIR) is represented as $$\{g_k\}_{k \geq 0} = \{g_0, g_1, ..., g_l, 0, 0, 0, ...\}$$, while an Infinite Impulse Response (IIR) is represented as $$\{g_k\}_{k \geq 0} = \{g_0, g_1, g_2, g_3, ...\}$$ and does not terminate. 

If $\{g_k\}_{k \geq 0}$ is a semi-infinite sequence where $g_k = 0$ for $k < 0$ (notice that FIR/IIR are all semi-infinite.) , then $y_k = \sum_{n=0}^{k} g_n u_{k-n}$, and the current output depends only on current and past inputs, making the LTI system causal.


# Causality

Systems operating as a function of time in real-time are always causal. However, "real-world systems" are not always causal. For example, in **image processing**, the sequence index $k$ often relates to pixel location rather than time, leading to non-causal systems. Signal processing systems operating on **stored or buffered data** can also work with non-causal systems, offering advantages. Signal storage and buffering enhance digital signal processing compared to continuous signal processing. 
	Control engineers prioritize real-time systems, making causality essential.



---

# Z-Tranform and DTFT

# Convolution and Polynomial Multiplication
The convolution of two finite length signals, $c = (c_0, c_1)$ and $u = (u_0, u_1, u_2)$, results in $y = c * u$, where:

$y_0 = c_0 u_0$
$y_1 = c_0 u_1 + c_1 u_0$
$y_2 = c_0 u_2 + c_1 u_1$
$y_3 = c_1 u_2$
$y_k = 0$ for $k < 0$ and for $k > 3$

This mirrors polynomial multiplication. If we have two polynomials $C(x) = c_0 + c_1x$ and $U(x) = u_0 + u_1x + u_2x^2$, their product $Y(x) = C(x)U(x)$ is:

$Y(x) = c_0u_0 + (c_0u_1 + c_1u_0)x + (c_0u_2 + c_1u_1)x^2 + (c_1u_2)x^3$

Semi-infinite sequences can be mapped to power series, such as $u(D) = u_0 + u_1D + u_2D^2 + u_3D^3...$. The convolution of semi-infinite sequences is equivalent to the multiplication of power series:
$$c(D)u(D) = (\sum_{k=0}^{\infty} c_kD^k)(\sum_{m=0}^{\infty} u_mD^m) = \sum_{k=0}^{\infty} \sum_{m=0}^{\infty} c_ku_mD^{k+m} = \sum_{k=0}^{\infty} \sum_{n=k}^{\infty} c_ku_{n-k}D^n = \sum_{n=0}^{\infty} (\sum_{k=0}^{n} c_ku_{n-k})D^n = \sum_{n=0}^{\infty} y_nD^n$$

where $y_n = \sum_{k=0}^{n} c_ku_{n-k}$, which means $y = c * u$.


So why transforming signals? 

Representing sequences as power series is a common technique in engineering and mathematics, used in generating functions in combinatorics, D-transforms in error correction, and **z-transforms and DTFT in digital control and signal processing**. 

**Power series** serve as substitute representations of sequences, hence the term "transform". 

# Representing sequences as power series
A formal power series uses a formal variable, such as $D$, **without assigning a value to it**. Formal power series harness computation rules for power series; 

for instance, $$\frac{1}{1-D} = 1 + D + D^2 + D^3...$$ always holds. Non-formal power series are only true if $|D| < 1$. 

Formal power series are sufficient for mapping convolutions to multiplications without assigning values or worrying about convergence, which is used for generating functions and D transforms. 

In z-transform/DTFT, a value is assigned to the variable $z/e^{j\theta}$, making it a power series (NOT a formal power series) with properties beyond converting convolutions to multiplications, such as **indicating stability and determining steady-state responses**.


# Z-transform

For a signal $\{u_k\}$, the z-transform is defined as $$U(z) = \sum_{k=0}^{\infty} u_k z^{-k}$$
This is equivalent to a generic transform with $D = z^{-1}$, adopting the negative power by analogy with the Laplace transform. 

The z-transform ignores signal values at negative times, although $\{u_k\}$ is **not assumed** to be one-sided. While the signal $\{u_k\}$ is real-valued in most control theory applications, it **can be complex** in others. 

The z-transform is used in wireless devices for signal processing applied to complex signals. Standard **z-transform properties are listed in the Information Data Book on page 3**.

## Examples
1. For the sequence $\mathbf{u} = \{u_k\}_{k \geq 0} = 1, 2, 3, 4, 5, 0, 0, 0, ...$, the z-transform is $$U(z) = 1 + 2z^{-1} + 3z^{-2} + 4z^{-3} + 5z^{-5}$$.

2. For the geometric sequence $\mathbf{u} = \{u_k\}_{k \geq 0} = \{1, q, q^2, q^3, q^4, ...\}$:
$$U(z) = \sum_{k=0}^{\infty} q^k z^{-k} = \sum_{k=0}^{\infty} (qz^{-1})^k = \frac{1}{1 - qz^{-1}} = \frac{z}{z - q}$$.This is valid if $|qz^{-1}| < 1$ or $|z| > |q|$, which defines the region of convergence (ROC) of the z-transform.

3. In the special case where $q = 1$, representing the unit step signal $\mathbf{u} = 1, 1, 1, ...$ (where $u_k = 0$ for $k < 0$ and $u_k = 1$ for $k \geq 0$):
$$U(z) = \frac{1}{1 - z^{-1}} = \frac{z}{z - 1}$$


# One-sided vs. two-sided

Most textbooks define the z-transform as a one-sided sum, but some use a two-sided sum from $-\infty$ to $\infty$, which is relevant for **stochastic signals analysis**. 

For example, $\{u_k\}_{k\geq0} = \{1, 1, 1, ...\}$ has a z-transform of $$U(z) = \frac{1}{1 - z^{-1}} = \frac{z}{z - 1}$$, while $\{v_k\}_{k<0} = \{..., 1, 1, 1\}$ has a z-transform of $$V(z) = \sum_{k=-\infty}^{-1} z^{-k} = \sum_{k=1}^{\infty} z^{k} = \frac{z}{z - 1}$$. These two signals have the same two-sided z-transform, distinguished only by their ROC: $|z| > 1$ for $U(z)$ and $|z| < 1$ for $V(z)$. For two-sided z-transforms, the ROC cannot be ignored. The two-sided transform is the DTFT.


# DTFT

For a signal $\{u_k\}$, the Discrete-Time Fourier Transform (DTFT) is defined as $$U(\theta) = \sum_{k=-\infty}^{\infty} u_k e^{-jk\theta}$$
Its properties are generally identical to the z-transform properties, and in some cases simpler (e.g., time shift properties). If a signal is zero for negative values, e.g., $\{u_k\}_{k\geq0}$, then $U(\theta) = U(z)$ for $z = e^{j\theta}$, i.e., $U(\theta) = U(e^{j\theta})$. 

For signals that are zero at non-negative values, the DTFT is **equivalent to the z-transform on the unit circle**.



# Linearity of the z transform and DTFT

For any scalars $\alpha, \beta$, the z-transform is linear:
$$Z[\alpha\{x_k\} + \beta\{y_k\}] = \alpha Z[\{x_k\}] + \beta Z[\{y_k\}]$$

If the signal definition involves a parameter $\alpha$, then $Z\left[\frac{d}{d\alpha} u_k\right] = \frac{d}{d\alpha} U(z)$.

The DTFT obeys the same properties.



We know that $Z[\{q^k\}_{k\geq0}] = \frac{1}{1 - qz^{-1}}$. Using the differentiation property of linearity:

$$Z\left[ \frac{d}{dq} [1, q, q^2, ...] \right] = Z[0, 1, 2q, 3q^2, ...] = \frac{d}{dq} \frac{1}{1 - qz^{-1}} = \frac{z^{-1}}{(1 - qz^{-1})^2}$$

The z-transform of the signal $u_0 = 0$, $u_k = kq^{k-1}$ for $k > 0$ is $\frac{z^{-1}}{(1 - qz^{-1})^2}$.

For the ramp sequence $[0, 1, 2, 3, ...]$, where $u_k = k$ for $k \geq 0$, the z-transform is $\frac{z^{-1}}{(1 - z^{-1})^2}$.

The differentiation trick can be used repeatedly to obtain $Z\left[ \frac{(k + m - 2)!}{(k - 1)!(m - 1)!} \right] = \frac{z^{-1}}{(1 - z^{-1})^m}$ for all $m \geq 1$.

Using linearity properties, the z-transform of $\cos \alpha k$ is:
$$Z[\cos \alpha k] = Z[\frac{1}{2}(e^{j\alpha k} + e^{-j\alpha k})] = \frac{1}{2} \left( \frac{1}{1 - e^{j\alpha} z^{-1}} + \frac{1}{1 - e^{-j\alpha} z^{-1}} \right) = \frac{1}{2} \frac{1 - e^{-j\alpha} z^{-1} + 1 - e^{j\alpha} z^{-1}}{(1 - e^{j\alpha})(1 - e^{-j\alpha})} = \frac{1 - z^{-1} \cos \alpha}{1 - 2z^{-1} \cos \alpha + z^{-2}}$$

Similarly, $Z[\sin \alpha k] = \frac{z^{-1} \sin \alpha}{1 - 2z^{-1} \cos \alpha + z^{-2}}$.

Scaling a sequence with a geometric sequence results in: $$Z[r^k u_k] = \sum_{k=0}^{\infty} u_k r^k z^{-k} = \sum_{k=0}^{\infty} u_k (r^{-1}z)^{-k} = U(r^{-1}z)$$
# Time shift properties of DTFT

Consider a sequence $\{u_k\}$ shifted by a delay $d$: $\mathbf{u'} = \{u_{k-d}\}$. The DTFT of the shifted sequence is $$U'(\theta) = \sum_{k=-\infty}^{\infty} u_{k-d} e^{-jk\theta} = \sum_{k'=-\infty}^{\infty} u_{k'} e^{-j(k'+d)\theta} = e^{-jd\theta} U(\theta)$$, where $k' = k - d$. Time shift for DTFT results in a multiplication by $e^{-j\theta d}$.


# Extending DTFT time-shift properties to the z transform

DTFT time shift results in multiplication by $e^{-j\theta d}$, and $U(\theta) = U(z)$ for $z = e^{j\theta}$ for signals that are zero at negative values. It's tempting to extend this to the z-transform as multiplication by $z^{-d}$. 

However, the z-transform's one-sided definition makes things trickier. 
- When delaying by a positive $d$, signal values formerly ignored at negative times now appear in the z-transform (unless $u_k = 0$ for $k < 0$). 
- When advancing by a negative $d$, signal values formerly at non-negative times must now be ignored because they end up at negative times.



## time delay

For a time delay where $\{u'_k\} = \{u_{k-d}\}$, the z-transform is $$Z[\{u_{k-d}\}] = \sum_{k=0}^{\infty} u_{k-d} z^{-k} = u_{-d} + u_{-(d-1)}z^{-1} + ... + u_{-1}z^{-(d-1)} + \sum_{k=d}^{\infty} u_{k-d}z^{-k} = u_{-d} + u_{-(d-1)}z^{-1} + ... + u_{-1}z^{-(d-1)} + \sum_{k'=0}^{\infty} u_{k'}z^{-(k'+d)} = u_{-d} + u_{-(d-1)}z^{-1} + ... + u_{-1}z^{-(d-1)} + z^{-d}U(z)$$.

For signals $\{u_k\}_{k\geq0}$ that are zero at negative values, $Z[\{u_{k-d}\}] = z^{-d}Z[\{u_k\}]$.

$z^{-1}$ is therefore the **time-delay operator**.

For a time advance where $\{u'_k\} = \{u_{k+d}\}$, the z-transform is $$Z[\{u_{k+d}\}] = \sum_{k=0}^{\infty} u_{k+d} z^{-k} = \sum_{k'=d}^{\infty} u_{k'} z^{-(k'-d)} = \sum_{k'=0}^{\infty} u_{k'} z^{-(k'-d)} - \sum_{k'=0}^{d-1} u_{k'} z^{-(k'-d)} = z^d U(z) - z^d u_0 - z^{d-1} u_1 - ... - zu_{d-1}$$

$z$ is the time-advance operator.

Time-shift properties can be used to adjust expressions for various sequences to obtain expressions in the *Information Data Book*, and can be applied repeatedly for a delay by $m$ or an advance by $m$.


# Initial Value Theorem

$\lim_{z \to \infty} U(z) = \lim_{z \to \infty} \sum_{k=0}^{\infty} u_k z^{-k} = \lim_{z \to \infty} (u_0 + \frac{u_1}{z} + \frac{u_2}{z^2} + ...) = u_0$



---

# Z-transform properties

The z-transform, similar to the Fourier transform, exhibits conjugate symmetry when applied to a real discrete-time signal $s$, where $$S(\overline{z}) = \overline{S(z)}$$
On the unit circle, this results in $|S(e^{-j\theta})| = |S(e^{j\theta})|$ and $\angle S(e^{-j\theta}) = -\angle S(e^{j\theta})$.


# Reverse symmetry property

The DTFT possesses a reverse symmetry property where, if $$s_{-k} = \overline{s_k}$$, then its DTFT $S(\theta)$ is **real**. 



# Inverse z transform

Several methods exist to invert the z-transform: 
- using partial fractions, 
- polynomial division, 
- Taylor expansion

The DTFT can be inverted using all the above methods, as well as the DTFT inversion formula: $$s_k = \frac{1}{2\pi} \int_{-\pi}^{\pi} S(\theta)e^{jk\theta} d\theta$$


# The DTFT and Fourier series

The DTFT is defined as $S(\theta) = \sum_{k=-\infty}^{\infty} s_k e^{-j\theta k}$ and $s_k = \frac{1}{2\pi} \int_{-\pi}^{\pi} S(\theta)e^{jk\theta} d\theta$

A complex Fourier Series (for $T = 2\pi$) is defined as $f(t) = \sum_{k=-\infty}^{\infty} c_k e^{jkt}$ and $c_k = \frac{1}{2\pi} \int_{-\pi}^{\pi} f(t)e^{-jkt} dt$

Fourier series, though not initially presented as a transform, possess transform-like properties, mapping **continuous periodic functions** to discrete coefficients, sharing properties like **conjugate symmetry and shift properties**. 

Fourier series are analogous to the DTFT (or z-transform on the unit circle) **with time and frequency interchanged**.



# The Laplace transform and the z transform

Applying the Laplace transform to a "train of impulses" sampled signal $w_s(t) = \sum_{k=0}^{\infty} w(kT)\delta(t - kT)$ yields $$W_s(s) = \sum_{k=0}^{\infty} w(kT)e^{-skT} = \sum_{k=0}^{\infty} w_k z^{-k}$$The z-transform is equivalent to the Laplace transform of the sampled "impulse train" signal, with a mapping from the Laplace domain to the z-domain defined by $s \rightarrow z = e^{sT}$.


---

# System transfer function & stability

A Linear Time-Invariant System (LTIS) described by linear difference equations in canonical form $$y_k + a_1y_{k-1} + ... + a_ny_{k-n} = b_0x_k + ... + b_mx_{k-m}$$, subject to zero initial conditions ($y_k = x_k = 0$ for $k < 0$),
gives in the z-domain $$Y(z) + a_1z^{-1}Y(z) + ... + a_nz^{-n}Y(z) = b_0X(z) + ... + b_mz^{-m}X(z)$$
and is hence described by a transfer function: $G(z) = \frac{Y(z)}{X(z)} = \frac{b_0 + b_1z^{-1} + ... + b_mz^{-m}}{1 + a_1z^{-1} + ... + a_nz^{-n}}$. This ratio is independent of $X(z)$.

![[Pasted image 20250331164253.png]]


# FIR/IIR in the z domain

- An FIR (finite impulse response) filter satisfies $a_n = 0$ for $n \neq 1$, meaning $G(z)$ has only a numerator and no denominator, making it a feed-forward only system where the output $y_k$ only depends on current and past values of the input $x_k, x_{k-1}, ...$ but not on past values of the output $y_{k-1}, y_{k-2}, ...$. 
- An IIR (infinite impulse response) filter has an infinite length delta response as a result of feedback.


# Delta response and poles

For a Linear Time-Invariant (LTI) system $G(z)$ with a delta input $\delta_k = (1, 0, 0, ...)$ which transforms to $\Delta(z) = 1$, the output $y$ can be defined as $$y = Z^{-1}[Y(z)] = Z^{-1}[G(z)\Delta(z)] = Z^{-1}[G(z)]$$The poles of $G(z)$ determine **the system's response to a pulse.**


![[Pasted image 20250331165146.png]]

![[Pasted image 20250331165219.png]]

# Properties

For a system with repeated poles, where $G(z) = \frac{1}{(1-pz^{-1})^2}$, it can be rewritten as $G(z) = \frac{1}{1-pz^{-1}} + \frac{pz^{-1}}{(1-pz^{-1})^2}$, and its inverse Z-transform is $p^k + kp^k$. 

The distance of poles from the origin indicates the decay rate, complex poles inside the unit circle result in lightly damped oscillation, and oscillation is possible for real poles on the negative real axis. A signal $\{u_k\}$ is considered bounded if there exists a positive constant $M$ such that $|u_k| < M$ for all $k$.


# BIBO Stability
A discrete-time system is considered stable in the Bounded Input Bounded Output (BIBO) sense if bounded inputs result in bounded outputs. 

**For any constant $M$, there exists a constant $N$ such that for any input signal bounded by $M$, the output is bounded by $N$.** 

If a bounded input produces an unbounded output, the system is unstable. Some unstable systems may not have a single unbounded output, but a collection of input signals bounded by $M$ can produce outputs that cannot be bounded by any single $N$.


# Theorem

For a discrete-time system $G$ with a rational transfer function $$G(z) = \frac{b(z)}{a(z)} = \frac{b_0 + ... + b_m z^{-m}}{1 + a_1 z^{-1} + ... + a_n z^{-n}}$$ with no common factors between $b(z)$ and $a(z)$, and a pulse response $\{g_k\}_{k \geq 0}$, the following conditions are equivalent: 
1. $G$ is stable, 
2. all roots $p_i$ of $a(z)$ (poles) satisfy $|p_i| < 1$, 
3. and $\sum_{k=0}^{\infty} |g_k|$ is finite. 

The logical sequence of proof is (1) implies (2), (2) implies (3), and (3) implies (1).


---

# Final value Theorem

If all poles of $(z - 1)Y(z)$ lie strictly inside the unit circle, then $$\lim_{k \to \infty} y_k = \lim_{z \to 1} (z - 1)Y(z)$$It is crucial to **verify the pole locations** of $(z - 1)Y(z)$ before applying the Final Value Theorem (FVT).



## steady-state response to a complex sinusoidal input
For a complex sinusoidal input $x_k = e^{j\theta k}$, the Z-transform is $X(z) = \frac{1}{1 - e^{j\theta}z^{-1}}$. Given a system $G(z) = \frac{b(z)}{(z-p_1)(z-p_2)...(z-p_n)}$, the output $Y(z) = G(z)X(z) = \frac{G(e^{j\theta})}{1 - e^{j\theta}z^{-1}} + \text{terms of the form } \frac{\beta_i}{1 - p_i z^{-1}}$. The output $y_k = G(e^{j\theta})e^{j\theta k} + \text{terms decaying to 0 as } k \to \infty$. The stationary output is $$\tilde{y}_k = G(e^{j\theta})e^{j\theta k} = |G(e^{j\theta})|e^{j(\theta k + \angle G(e^{j\theta}))}$$


## steady-state response to a real sinusoidal input

For a real sinusoidal input $x_k = \cos(\theta k) = \frac{1}{2}(e^{j\theta k} + e^{-j\theta k})$, the stationary output $\tilde{y}_k$ is given by $\tilde{y}_k = \frac{|G(e^{j\theta})|}{2}(e^{j(\theta k + \angle G(e^{j\theta}))} + e^{-j(\theta k + \angle G(e^{j\theta}))}) = |G(e^{j\theta})|\cos(\theta k + \angle G(e^{j\theta}))$. The filter attenuates the sinusoidal input $\cos(\theta k)$ by a factor $|G(e^{j\theta})|$ and shifts its phase by a factor $\angle G(e^{j\theta})$.



# Bode diagrams

For an input $x_k = \cos(\theta k)$, the steady-state output is $\tilde{y}_k = |G(e^{j\theta})|\cos(\theta k + \angle G(e^{j\theta}))$. 

Filter amplification and phase shift can be characterized at each frequency using Bode diagrams. 

![[Pasted image 20250331174941.png]]

Bode diagrams provide a good representation of system behavior since every input signal can be decomposed into a sum of sinusoids.

Since $\cos(\theta k) = \cos((\theta + 2\pi)k)$, **going more than a complete revolution is redundant**. Negative frequencies mirror positive frequencies for real-valued signals, so Bode diagrams are generally limited to the frequency interval $[0, \pi]$.

![[Pasted image 20250331175152.png]]


Hints:
*   **Magnitude Response:** Product of distances from zeros to $e^{j\theta}$ divided by product of distances from poles to $e^{j\theta}$ (sums/subtractions in dB).
*   **Phase Response:** Sum of angles from zeros to $e^{j\theta}$ minus sum of angles from poles to $e^{j\theta}$.
*   **Resonance/Null:** Proximity of $e^{j\theta}$ to a pole causes resonance, to a zero causes a null.
*   **Digital Systems:** No simple rules for Bode diagrams; use numerical tools.


## To log or not to log

*   **Continuous-time Bode plots:** Use logarithmic frequency scale (0 to $\infty$).
*   **Discrete-time Bode plots:** Choice of linear or logarithmic frequency scale (0 to $\pi$ normalized, 0 to $f_s/2$ actual) depends on the application.

---

# Nyquist stability theorem

The closed-loop system is stable if and only if the number of encirclements of $-\frac{1}{K}$ by $G(e^{j\theta})$ as $\theta$ increases from $-\pi$ to $\pi$ equals the number of open-loop poles strictly outside the unit circle.

$$\boxed{\text{Stability} \iff \text{Enc}(-\frac{1}{K}, G(e^{j\theta})) = \text{Poles outside unit circle}}$$

The proof of the Nyquist stability criterion involves these steps:

1.  Poles/zeros and encirclements of the origin.
2.  Counting encirclements of the origin.
3.  Poles and zeros of $1 + KG(z)$ and corresponding encirclements.
4.  Polynomial degrees vs. numbers of poles/zeros.
5.  Pole arithmetic: how do closed and open loop stable/unstable poles add up?
6.  Shifting the graph to $-1/K$.
7.  The Nyquist criterion.


## The encirclement property

![[Pasted image 20250331180704.png]]


*   **Zeros inside unit circle:** Angle of $G(e^{j\theta})$ goes from 0 to $2\pi$ (counter-clockwise).
*   **Poles inside unit circle:** Angle of $G(e^{j\theta})$ goes from 0 to $-2\pi$ (clockwise).
*   **Zeros/poles on unit circle:** Phase jumps by $\pi$ or $-\pi$, causing encirclement.
*   **Encirclement behavior:** "Passes through infinity" in the complex plane.

Let $N_{z,i}$ be the number of zeros of $F(z)$ inside the unit circle, and $N_{p,i}$ be the number of poles of $F(z)$ inside the unit circle (including the unit circle). 

The overall increase $\alpha$ of $\angle F(e^{j\theta})$ as $\theta$ increases from 0 to $2\pi$ (or $-\pi$ to $\pi$) is $$\alpha = 2\pi(N_{z,i} - N_{p,i})$$
The number of encirclements $C$ of the origin is $C = N_{z,i} - N_{p,i}$.



## Closed loop stability

Given $1 + KG(z) = \frac{a(z) + Kb(z)}{a(z)}$, where the closed-loop poles are solutions of $1 + KG(z) = 0$:

*   The zeros of $1 + KG(z)$ (when $a(z) + Kb(z) = 0$) are the $\boxed{\text{closed loop poles}}$.
*   The poles of $1 + KG(z)$ (when $a(z) = 0$) are the $\boxed{\text{open loop poles}}$.

Let $N_{z,i}$ and $N_{p,i}$ be the number of zeros and poles of $1 + KG(z)$ inside the unit circle, respectively. Then $N_{cp,i} = N_{z,i}$ is the number of $\boxed{\text{closed loop poles}}$ inside the unit circle, and $N_{op,i} = N_{p,i}$ is the number of $\boxed{\text{open loop poles}}$ inside the unit circle. 

The number of encirclement $C$ of the origin by $1 + KG(e^{j\theta})$ is $$C = N_{z,i} - N_{p,i} = N_{cp,i} - N_{op,i}$$

# Methodology of nyquist theorem

1.  Draw a pole-zero diagram of the open-loop system $G(z)$.
2.  Count poles strictly outside the unit circle: this is the number $C$ of encirclements of $-1/K$ necessary to achieve stability.
3.  Draw the Nyquist locus of $G(e^{j\theta})$ for $\theta$ from 0 to $\pi$.
4.  Work out the values of $G(e^{j\theta})$ for $\theta = 0$, $\theta = \pi$ and any key points of interest and annotate those on the graph.
5.  Complete the graph for $\theta$ from $\pi$ to $2\pi$ (or, equivalently, $-\pi$ to 0) by symmetry.
6.  If the open loop system has poles on the unit circle, work out the asymptotes as the locus goes to infinity.
7.  Apply the Nyquist stability criterion to determine range(s) of $K$ for which the closed loop system is stable.

To easily remember the Nyquist stability criterion methodology, think of it as a 7-step process:

1.  **Diagram:** Draw the pole-zero diagram.
2.  **Count:** Count unstable poles (outside the unit circle).
3.  **Locus:** Sketch the Nyquist locus (0 to $\pi$).
4.  **Values:** Find key values on the locus.
5.  **Symmetry:** Complete the locus by symmetry.
6.  **Asymptotes:** Consider poles on the unit circle and asymptotes.
7.  **Criterion:** Apply the Nyquist criterion to find the stable range of K.

A mnemonic could be: **D**on't **C**all **L**awyers, **V**alue **S**afety, **A**lways **C**areful.


## Strictly inside/outside?
For the Nyquist stability criterion, zeros/poles on the unit circle are considered "inside" for the proof because they cause encirclements similar to those inside the unit circle. 

However, excluding only closed-loop poles strictly outside the unit circle isn't entirely accurate when expressing closed-loop system stability. Closed loop poles on the unit circle correspond to an unstable open loop pole, but can be excluded because they will be on the boundary of the stable ranges of $K$, which are **defined by strict inequalities**.

For open loop poles, on the unit circles means the close loop poles are within the unit circle. So for the pole zero diagram, we need to draw the unit circle in such way that include poles on the unit circle, like below:

![[25641.png]]



---

# Continuous to Discrete Mappings and Interfaces

- Purpose: mapping between Laplace (continuous) and z (discrete domains)























