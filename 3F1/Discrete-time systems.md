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
A formal power series uses a formal variable, such as $D$, without assigning a value to it. Formal power series harness computation rules for power series; 

for instance, $$\frac{1}{1-D} = 1 + D + D^2 + D^3...$$ always holds. Non-formal power series are only true if $|D| < 1$. 

Formal power series are sufficient for mapping convolutions to multiplications without assigning values or worrying about convergence, which is used for generating functions and D transforms. In z-transform/DTFT, a value is assigned to the variable $z/e^{j\theta}$, making it a power series with properties beyond converting convolutions to multiplications, such as indicating stability and determining steady-state responses.






















