# Millimeter Wave Channel

[TOC]

Millimeter wave channel refers to the transmission channel for wireless communication in the millimeter wave frequency band. This frequency band is located in the high-frequency part of the radio spectrum, typically between 30 GHz and 300 GHz. Due to the characteristics of these frequencies, millimeter wave communication has a high bandwidth and data transmission speed, but signals are subject to strong attenuation and blocking effects when propagating in space.

- High bandwidth: Millimeter wave channels provide a large amount of available spectrum and can support high-speed data transmission.

- Low latency: Due to the high-speed transmission of signals, millimeter wave communication typically has low latency and is suitable for real-time applications.

- Short transmission distance: Millimeter wave signals quickly decay when propagated in the air, so they are usually used for short distance communication, such as inter cell communication or indoor coverage.

- Poor blocking and penetration ability: Millimeter wave signals are greatly affected by obstacles (such as buildings, rain, snow, etc.), resulting in poor signal penetration ability and the need for multipath propagation to improve reliability.

## Model

### Path Loss

### Channel matrix

$$
\boldsymbol H = \frac{N_t N_r}{N_\text{cluster} N_\text{ray}} \sum_{i,l} α_{i,l} Λ_r(\phi_{r,i,l}, \theta_{r,i,l}) Λ_t(\phi_{t,i,l}, \theta_{t,i,l}) \boldsymbol a_r(\phi_{r,i,l}, \theta_{r,i,l}) \boldsymbol a_t(\phi_{t,i,l}, \theta_{t,i,l})^T
$$

- $H$：这是通道矩阵，表示通信信道的特性，通常是一个复数矩阵。
- $Nt$ 和 $Nr$：分别表示发射天线和接收天线的数量。
- $Ncluster$ 和 $Nray$：分别表示信号簇数和射线数，通常用于描述多径传播环境中的信道。
- $αi,l$：这是一个系数，可能表示每个信号路径的路径增益。
- $Λr(φr,i,l, θr,i,l)$ 和 $Λt(φt,i,l, θt,i,l)$：这可能是表示接收和发射天线的方向性增益的函数，通常与天线指向（方位角和俯仰角）有关。
- $ar(φr,i,l, θr,i,l)$ 和 $at(φt,i,l, θt,i,l)$：这是表示接收和发射天线的天线模式向量，通常与天线的方向性和极化特性有关
- $α_{i,l}$ Complex channel gain, For $l^{th}$ ray of $i^{th}$ Scattering cluster
- $\boldsymbol a_r(\phi_{r,i,l}, \theta_{r,i,l}) \boldsymbol a_t(\phi_{t,i,l}, \theta_{t,i,l})$ Array factor  


The array factor represents the phase difference between each sub antenna and the reference antenna in the array antenna

- Note  
    When the target is far enough away, the angular difference in antenna direction can be ignored There will be a small distance difference between different antennas, resulting in a phase difference.
    $$
    \begin{align*}
    \boldsymbol a_{ULA} (\phi) &= \frac{1}{\sqrt{N}} (1, ... , e^{jkd (n-1) \sin(\phi)}, ... , e^{jkd (N-1) \sin(\phi)})^T  \tag{linear array antenna}  \\
    \boldsymbol a_{UPA} (\phi,\theta) &= \frac{1}{\sqrt{N}} (1, ... , e^{jkd ((m-1) \sin(\phi) \sin(\theta) + (n-1) cos(\theta))}, ... , e^{jkd ((W-1) \sin(\phi) \sin(\theta) + (H-1) cos(\theta))})^T  \tag{Area array antenna}
    \end{align*}
    $$

- Proof
    Reference antenna radiation 
    $$
    \boldsymbol x = \boldsymbol a t
    $$

    Sub-antenna coordinates 
    $$
    \boldsymbol x_0 = (\Delta x, \Delta y, \Delta z)^T
    $$

    Subantenna isosurface 
    $$
    \boldsymbol a^T (\boldsymbol x - \boldsymbol x_0) = 0
    $$

    The intersection of the reference point ray and the sub antenna isosurface, solving $t$, and $t $is the path difference between the sub antenna and the reference antenna ray
    $$
    \begin{align*}
    \boldsymbol a^T (\boldsymbol a t - \boldsymbol x_0) &= 0  \tag{substitution}  \\
    \boldsymbol a^T \boldsymbol a t &= \boldsymbol a^T \boldsymbol x_0  \\
    \Rightarrow\quad t &= \boldsymbol a^T \boldsymbol x_0  \\
    &= \left(\begin{matrix} \sin \theta \cos \phi \\ \sin \theta \sin \phi \\ \cos \theta \end{matrix}\right) \left(\begin{matrix} \Delta x & \Delta y & \Delta z \end{matrix}\right)  \tag{Spherical coordinate}   \\
    &= \Delta x \sin \theta \cos \phi + \Delta y \sin \theta \sin \phi + \Delta z \cos \theta
    \end{align*}
    $$

### Multi antenna channel calculation

- 算法详述
- 两个天线时
- 当目标足够远时，天线方向的角度差异可以忽略。
- 不同天线之间会存在一小段距离差，从而带来相位差。

- 线阵天线时
- 面阵天线时

### Saleh-Valenzuela Model
- 到达角、发送角范围
- 散射簇所在的到达角、发送角
- 散射簇散射的子径的到达角、发送角
- 每个子天线的位置
- 阵列响应矢量
- 增益因子
- 信道矩阵