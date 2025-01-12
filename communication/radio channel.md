# Radio Channel
[TOC]
Radio channel is a channel that uses electromagnetic waves as a transmission medium.

无线通信信道的特性主要包括信道强度随时间和频率的变化。这些变化可以大致分为两种类型：

- 大尺度衰落：由于信号作为距离函数的路径损失和大物体（如建筑物和山丘）的阴影引起的。这种情况发生在移动设备通过与单元大小相当的距离时，通常是频率独立的。

- 小尺度衰落：由于发射机和接收机之间的多个信号路径的构造和破坏干涉引起的。这种情况发生在空间尺度上，其顺序为载波波长，并且是频率相关的。

发送信号
$$
x(t) = Re( s(t) e^{j2π f_c t} )
$$
- $e^{j 2 π f_c t}$ 载波

接受信号
$$
y(t) = h(t) * x(t) + n(t)
$$

- $h(t)$ 信道冲激响应
- $n(t)$ 噪声




### Signal fading
$$
y(t) = Re( \sum_{i=1}^{N_{path}(t)} α_i(t) s(t - τ_i(t)) e^{j( 2π f_c (t - τ_i(t)) + φ_{D_i}(t) )} ) + n(t)
$$
$$
h(t) = \sum_{i=1}^{N_{path}(t)} α_i(t) δ(t - τ_i(t)) e^{j( 2π f_c (t - τ_i(t)) + φ_{D_i}(t) )}
$$

- $N_{path}(t)$ 多径数量
- $α_i(t)$ 幅度. 基于 路径损耗、阴影衰落 $P_L = \frac{P_r}{P_t}$
- $τ_i(t)$ 时延. $τ_i(t) = \frac{r_i(t)}{c}$
- $φ_{D_i(t)}$ Doppler相移. $f_{D_i(t)} = \frac{v \cos(θ(t))}{λ},\quad φ_{D_i(t)} = \int_t 2 π f_{D_i(τ)} \d τ$
- $α_i(t), τ_i(t), φ_{D_i(t)}$ 是平稳遍历随机过程.

### Path loss
$$
P_L = \frac{P_r}{P_t}
$$
- 参考距离
$L(d) = L(d_{ref}) + 10 n \log_{10} \frac{d}{d_{ref}}  \tag{dB式}$
- $n$ 路径损耗指数. 自由空间下$n = 2$.
\Example
- 自由空间路径损耗
$$
r(t) = Re( \frac{\sqrt(G_l) λ}{4 π d} u(t) e^{j 2 π f_c t} )
L = (\frac{4 π d}{λ})^2
= 20 \log_{10}(\frac{4 π}{c}) + 20 \log_{10} f + 20 \log_{10} d  \tag{dB式}
$$

### Doppler shift
$$
f_D = \frac{1}{2 π} \frac{Δ φ}{Δ t} = \frac{v}{λ} \cos θ
$$

### Propagation characteristics
#### Reflection
$$
L = (\frac{4 π d}{λ})^2 |1 + \sum R_i e^{j ΔΦ_i}|^2  \tag{直射波+多径一次反射波}
ΔΦ = \frac{2 π Δl}{λ}
$$
当多径数目很大时, 公式无法准确计算, 必须用统计方法计算接收信号功率.
* 绕射
* 散射

### Shadow Fading

$$
L(d) = L(d_{ref}) + 10 n \log_{10} \frac{d}{d_{ref}} + \xi_{σ}  \tag{$\xi_{σ}$阴影衰落}
$$
电磁波在传播路径上受到建筑物等阻挡所产生阴影效应而产生衰落, 反映中等范围内(数百波长级)接收信号电平平均值起伏变化趋势.

### Multipath Fading

## Empirical Model
### Outdoor Propagation Empirical Model
**Okumura-Hata**
$$
L(d) = L_\text{free space}(f_c, d) + A_μ(f_c, d) - G(h_t) - G(h_r) - G_\text{AREA}
G(h_t) = 20 \log_{10} (h_t / 200) \qu, h_t \in (30m, 1000m)
G(h_r) = \left\{\mb
10 \log_{10} (h_r / 3) \qu, h_r ≤ 3m
20 \log_{10} (h_r / 3) \qu, h_r \in (3m, 10m)
\me\right.
$$
$$
L = 69.55 + 26.16 · \log_{10}(f_c) - 13.82 · \log_{10}(h_t) - α(h_r) + (44.9 - 6.55 · \log_{10}(h_t)) · \log_{10}(d / 1000)
α(h_r) = \left\{\mb
8.29 · (\log_{10}(1.54 h_r))^2 - 1.1  \qu,  fc ≤ 300E6
3.2 · (\log_{10}(11.75 h_r))^2 - 4.97  \qu, fc > 300E6
(1.1 · \log_{10}(fc) - 0.7) · h_r - (1.56 · \log_{10}(fc) - 0.8)  \qu, \text{中小城市}
\me\right.
$$

**COST-231-Hata **			

**CCIR **
自由空间路径损耗和地形引入的路径损耗联合效果的经验公式.

**LEE **

**COST-231-Walfisch-Ikegami **

### Narrowband & broadband fading channels
Narrowband fading
$$
T_m << B^{-1}
$$
所有路径的时延都远小于信道带宽的倒数.

简化, 因为$T_m << B^{-1}$
$$
u(t - τ_i) = u(t)\\
y(t) = Re(u(t) e^{j2π f_c t} (\sum α_i(t) e^{-j φ_i(t)})) \\
φ_i(t) = 2π f_c τ_i(t) - φ_{D_i}(t) - φ_0
$$

Rayleigh Decline
无直射信道存在, 当$N(t)$足够大时, $y_I(t), y_Q(t) \to Gauss$, $|y| = \sqrt(y_I(t)^2 + y_Q(t)^2) \to Rayleigh$ 
$$
X, Y ~ Gauss
\sqrt{X^2 + Y^2} ~ Rayleigh
X^2 + Y^2 ~ Exp
$$

Rician Decline
当直射路径存在时
$$
\mathbb P(x) = \frac{x}{σ^2} e^{\frac{-(x^2 + s^2)}{2 σ^2}} I_0{\frac{x s}{σ^2}}
= \frac{2x(K+1)}{\bar P_r} e^{-K-\frac{(K+1) x^2}{\bar P_r}} I_0(2x \sqrt{\frac{K (K+1)}{\bar P_r}})
$$

- $K = \frac{s^2}{2 σ^2}$ 直射-非直射功率比. $K = 0$ Rayleigh衰落; $K \to \infty$ 无衰落.
- $r$信号包络
- $I_0()$ 零阶第一类修正Bessel函数.

broadband fading