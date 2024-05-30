# Visible Light Communication Channel

[TOC]

## Model

### Equivalent Baseband Model
$$
y(t) = x(t) \cdot h(t) + n(t)
$$

- $x(t)$ Is optical power (not amplitude in RF). constraint condition,
- $x(t) \ge 0$ 
- $P_{max}$  (Consider human eye safety).
- Line of sight transmission model
$$
\begin{align*}
h_{LoS}(t) &= \frac{A_r (m+1)}{2 \pi d^2} \cos^m(\phi) T_s(\Psi) g(\Psi) \cos(\Psi) \delta(t - d/c)  \tag{Channel impulse response}\\
SNR &= \frac{(P G K)^2}{B N}  \tag{Signal-to-noise ratio}  
\end{align*}
$$
- Lambert Angular distribution of radiation intensity
$$
\begin{align*}
R_0(\phi) = \left\{\begin{matrix}
\frac{m+1}{2 \pi} \cos^m(\phi) \quad, \phi \in [-\pi/2, \pi/2]\\
0 \quad, other.  \\
\end{matrix}\right.
\end{align*}
$$

- Lambert Emission level: Indicates beam directionality.
$$
m = \frac{- \ln 2}{\ln (\cos \Psi_{1/2})}
$$

- $\Psi_{1/2}$ Half power half angle
- 辐射强度 
$$
S(\phi) = P_t \frac{m + 1}{2 \pi} \cos^m(\phi)
$$

- Effective acceptance area
$$
A_{eff} = A_r \cos(\Psi) \quad, \Psi \in [0, \frac{\pi}{2}]
$$

- Non imaging condenser
$$
\begin{align*}
g(\Psi) &= \left\{\begin{matrix}
\frac{n^2}{sin^2 \Psi_c}  \quad, \Psi \in [0, \Psi_c]  \\
0  \quad, \Psi > \Psi_c
\end{matrix}\right.
\end{align*}
$$

- Relationship between receiving field angle of view, lens receiving area, and photodetector receiving area
$$
A_\text{coll} \sin \frac{\Psi_c}{2} \le A_r
$$


### Non line of sight transmission model

* Ceiling reflection model
* Hayasak-Ito model
* spherical model

### Outdoor atmospheric channel

- Note
  atmospheric turbulence