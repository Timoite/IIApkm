# Continuous to Discrete Mappings and Interfaces

- Purpose: mapping between Laplace (continuous) and z (discrete domains)
	- transfer analog design to digital
	- Model hybrid system systems 


## Algebraic transformation
Linear approximation of $e^{sT}$ gives $1+sT$, so:
$$
s= \frac{z-1}{T}
$$
We can replace $s$ in a continuous time system by this equation. 

Common algebraic transformation involves more than that. There are three types:
1. Euler's method for **Forward difference**: $s= \frac{z-1}{T}$
2. Backward difference: $s= \frac{1-z^{-1}}{T}$
3. Bilinear (Tustin's) Transformation: $s= \frac{2}{T} \frac{z-1}{z+1}$ or simply $\frac{z-1}{z+1}$, it works better as this is a trick for approximating quadratically.

![[Pasted image 20250401173906.png]]

Forward could be unstable, while backward is always stable, so does Tustin.


# Bilinear Transform and Frequency Warping Summary

The bilinear transform maps between continuous-time (s-domain) and discrete-time (z-domain) systems using the relationship:
$s = \frac{2}{T} \cdot \frac{z-1}{z+1}$ or $s = \frac{z-1}{z+1}$ (normalized)


# Bilinear Transform and Frequency Warping Summary

The bilinear transform maps between continuous-time (s-domain) and discrete-time (z-domain) systems using the relationship:
$$s = \frac{2}{T} \cdot \frac{z-1}{z+1}$$ 
or in normalized form:
$$s = \frac{z-1}{z+1}$$

## Key Points to Remember:

- **Stability Preservation**: The bilinear transform preserves stability properties. Points in the left half of the s-plane ($\lambda < 0$) map to inside the unit circle in the z-plane ($|z| < 1$), maintaining stability.

- **Frequency Warping**: The transform introduces a nonlinear distortion in the frequency response. The relationship between analog frequency ($\omega$) and digital frequency ($\theta$) is:
  $$\omega = \tan\left(\frac{\theta}{2}\right)$$ and $$\theta = 2\arctan(\omega)$$

- **Frequency Response Mapping**: If an analog filter has frequency response $G_c(j\omega)$, the corresponding digital filter's frequency response is:
  $$G(e^{j\theta}) = G_c\left(j\tan\left(\frac{\theta}{2}\right)\right)$$

- **Pre-warping**: When designing digital filters with specific cutoff frequencies, you must pre-warp the desired digital cutoff frequency using $\theta = 2\arctan(\omega)$ to find the corresponding analog cutoff frequency before applying the transform.

- **Normalized Response**: The normalized frequency response of the digital filter ($|\theta|\leq \pi$) is given by:
  $$G(e^{j\theta}) = G_c(\psi(e^{j\theta}))$$ where $$\psi(e^{j\theta}) = j\tan\left(\frac{\theta}{2}\right)$$

<details><summary>Thinking</summary>
Let me explain prewarping in the context of bilinear transform and outline the key steps for designing a digital filter to mimic an analog filter design.

## Prewarping

Prewarping is a technique used to compensate for the frequency warping effect introduced by the bilinear transform. The bilinear transform maps the entire analog frequency axis (-∞ to +∞) onto the digital frequency range (-π to π), which creates a nonlinear mapping between analog frequencies and digital frequencies.

When we're designing a digital filter to match an analog filter at specific frequencies (like cutoff frequencies), we need to adjust for this nonlinear relationship. Without prewarping, a cutoff frequency of ωc in the analog domain would not map to the expected corresponding digital frequency.

The warping relationship is:
ω = tan(θ/2) or θ = 2·arctan(ω)

where:
- ω is the analog frequency
- θ is the digital frequency

Prewarping involves using this relationship to calculate the correct analog frequency to use in the design process so that after the bilinear transform, the digital filter will have the desired frequency response at the specified digital frequencies.

## Key Steps to Design a Digital Filter to Mimic an Analog Filter

4. **Specify Requirements**: Determine the desired specifications for the digital filter (cutoff frequencies, passband ripple, stopband attenuation, etc.)

5. **Prewarp Critical Frequencies**: Convert the desired digital cutoff/critical frequencies (θc) to the corresponding analog frequencies (ωc) using:
   ωc = tan(θc/2)

6. **Design an Analog Filter**: Using the prewarped analog frequencies, design an analog filter that meets the specifications (Butterworth, Chebyshev, etc.)

7. **Apply Bilinear Transform**: Convert the analog filter to a digital filter using the bilinear transform:
   s = (2/T)·(z-1)/(z+1) or s = (z-1)/(z+1) in normalized form

8. **Verify the Design**: Check that the resulting digital filter meets the original requirements at the desired digital frequencies

This process ensures that the digital filter correctly matches the analog filter characteristics at the specified frequencies, compensating for the warping effect of the bilinear transform.
# ---</details>

# Prewarping in Bilinear Transform

**Prewarping** is a technique that compensates for frequency distortion introduced by the bilinear transform. 

## What it does:
- Corrects the nonlinear frequency mapping between analog and digital domains
- Ensures critical frequencies (like cutoff points) in the digital filter match exactly with the specified analog frequencies
- Uses the relationship: $$\omega_a = \tan\left(\frac{\omega_d}{2}\right)$$
  where $\omega_a$ is the analog frequency and $\omega_d$ is the desired digital frequency

## Generalized Steps to Design a Digital Filter from Analog Filter

9. **Specify Requirements**: Define desired digital filter specifications (cutoff frequencies, passband/stopband characteristics)

10. **Prewarp Critical Frequencies**: Convert digital frequencies to analog frequencies using:
   $$\omega_a = \tan\left(\frac{\omega_d}{2}\right)$$

11. **Design Analog Filter**: Create an analog transfer function $H(s)$ using the prewarped frequencies

12. **Apply Bilinear Transform**: Convert to digital domain by substituting:
   $$s = \frac{2}{T}\frac{z-1}{z+1}$$ 
   or $$s = \frac{z-1}{z+1}$$ (normalized)

13. **Simplify**: Algebraically manipulate to obtain the digital filter transfer function $H(z)$

14. **Implement**: Convert $H(z)$ to difference equation or filter coefficients for implementation


## Response matching
- Intuitive way of sampling continuous signal in time domain