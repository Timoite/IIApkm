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










