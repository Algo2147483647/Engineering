# Modulation & Demodulation

[TOC]

调制是将信息放在载波的方法. 分析调制性能的指标是频谱宽度, 功率, 功率效率.

## Analog Modulation

模拟消息信号直接调制在载波上，让载波的特性跟随其幅度进行变化

发送信号 $f(t)$, 载波$\cos(\omega_c t)$

正弦载波有三个参量: 幅度, 频率, 相位. 模拟调制就是将信息放在其中一个参量上.

**Amplitude Modulation (AM)**
$$
s_{AM}(t) = (A_0 + f(t)) \cdot \cos(\omega_c t)\\
S_{AM}(\omega) = \pi A_0(\delta(\omega - \omega_c) + \delta(\omega + \omega_c)) + \frac{1}{2}(F(\omega - \omega_c) + F(\omega + \omega_c))
$$
有用功率
$$
\eta_{AM} = \frac{P_f}{P_{s}} = \frac{\bar{m^2(t)}}{A_0^2+ m^2(t)}
$$

**双边带调制**
$$
s_{DSB}(t) = f(t)  \cos(\omega_c t)\\
S_{DSB}(\omega) = \frac{1}{2}(F(\omega - \omega_c) + F(\omega + \omega_c))
$$


解调方法: 相干解调

**单边带调制**
$$
s_{SSB}(t) = \frac{1}{2} f(t) \cos (\omega_c t) \mp \frac{1}{2} \hat f (t) \sin (\omega_c t)\\
S_{SSD}(\omega) = S_{DSB}(\omega) \cdot H(\omega)\\
H(\omega)=\left\{\begin{array}{ll}
1 & |\omega|>\omega_{c} \\
0 & |\omega| \leqslant \omega_{c}
\end{array}\right.
$$
其中 $\hat f(t)$ 是$f(t)$的希尔伯特变换

**残留边带调制 VSB**

**Frequency Modulation (FM)**
$$
s_{FM}(t) = A\cos\left(\omega_c t + K_{FM} \int f(\tau) \mathrm{d} \tau\right)\\
$$
**Phase Modulation (PM)**
$$
s_{PM}(t) = A\cos(\omega_c t + K_{PM} f(t))
$$

### 解调制

相干解调

包络检波

## Digital Modulation

**Amplitude Shift Keying Modulation**

把二进制符号0和1分别用不同的幅度来表示
$$
s_{2FSK}(t)=\left\{\begin{array}{ll}
A \cos \left(\omega_{c} t\right) & \text {send } 1\\
0 & \text {send } 0
\end{array}\right.
$$


**Frequency Shift Keying Modulation**

用不同的频率来表示不同的符号.
$$
s_{2FSK}(t)=\left\{\begin{array}{ll}
A \cos \left(\omega_{1} t+\varphi_{n}\right) & \text {send } 1\\
A \cos \left(\omega_{2} t+\theta_{n}\right) & \text {send } 0
\end{array}\right.
$$


**Phase Shift Keying Modulation**

通过二进制符号0和1来判断信号前后相位.
$$
s_{2PSK}(t)=\left\{\begin{array}{ll}
A \cos \left(\omega_{c} t+0\right) & \text {send } 1\\
A \cos \left(\omega_{c} t+\pi\right) & \text {send } 0
\end{array}\right.\\
s_{mPSK}(t)=A \cos \left(\omega_{c} t+\frac{2\pi(k-1)}{m}\right) & \text {send } 1
$$


**Quadrature Amplitude Modulation**

利用正交载波对两路信号分别进行双边带抑制载波调幅形成的. 振幅和相位作为两个独立的参量同时受到调制
$$
s_{QAM} = A_k \cos(\omega_0 t + \theta_k)
$$
**Gaussian Frequency Shift Keying**

在调制之前通过一个高斯低通滤波器来限制信号的频谱宽度.

**最小频移键控 Minimum Frequency Shift Keying**

**Orthogonal Frequency Division Multiplexing**

在多个载波频率上编码数字数据
$$
s_{OFDM}(t) = \sum_{k=0}^{N-1}B_k e^{i2\pi f_k t+ \varphi_k}
$$
