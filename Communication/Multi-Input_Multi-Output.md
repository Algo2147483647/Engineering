# Multi-Input Multi-Output

[TOC]
## 场景
- 发送天线 $N_t$个
- 接收天线 $N_r$个

- 信道矩阵 $\boldsymbol H$

- 接收信号
$$
\boldsymbol y = \boldsymbol H \boldsymbol x + \boldsymbol z \quad ; z ~ N(\boldsymbol μ, \boldsymbol Σ_Z)
$$

### 信道容量
$$
C = \max_{\boldsymbol R_{xx}} \log_2 |\boldsymbol I + \frac{P_x}{P_z} · \boldsymbol H \boldsymbol R_{xx} \boldsymbol H^H|
$$


发送机预编码$V$, 接收机预编码$U^H$
$$
\begin{align*}
C &= \sum_i^{N_r} \log(1 + \frac{P_i^* σ_i}{σ_z^2})  \\
P_i^* &= \max\{ 0, \frac{1}{ν^*} - α_i \}  \\
\sum P_i^* &= P_x  \\
\end{align*}
$$

静态信道

- 发送端、接收端知道$H$时

$$
C = \max_{\rho} \sum B \log_2 (1 + σ_i^2 \rho_i)
$$

- 发送端不知道$H$时

- 衰落信道
- 发送端、接收端知道$H$时
$$
C = \mathbb E_H( \max_{R_{xx} |_{Tr(R_{xx} = \rho)} } B \log_2 ( 1 + \frac{P_i \gamma_i}{P} ) )
$$

- Proof
$$
\begin{align*}
C &= \max I(X;Y)  \tag{定义} \\
&= \max ( H(Y) - H(Y|X) ) \\
&= \max ( H(Y) - H(H X + Z|X) ) \\
&= \max ( H(Y) - H(Z) )  \tag{$X,Z$统计独立} \\
&= \max ( H(Y) ) - N/2 \log (2 π e |\boldsymbol Σ_Z|^{1/N})
\end{align*}
$$
- $H(Y)$取最大时达到信道容量. 平均功率受限的随机变量, 当$Y$为循环对称复Gauss分布时, $H(Y)$ 取得最大值.
$$
\begin{align*}
\Rightarrow C &= \max_{\boldsymbol Σ_Y} N/2 \log(2 π e |\boldsymbol Σ_Y|^{1/N}) - N/2 \log (2 π e |\boldsymbol Σ_Z|^{1/N}) \\
&= \max_{\boldsymbol Σ_Y} 1/2 \log \frac{|\boldsymbol Σ_Y|}{|\boldsymbol Σ_Z|}
\end{align*}
$$
- $y$的自协方差矩阵
$$
\begin{align*}
\boldsymbol Σ_Y &= E((\boldsymbol y - \bar {\boldsymbol y}) (y - \bar {\boldsymbol y})^H)  \tag{定义}  \\
&= E(\boldsymbol y \boldsymbol y^H)  \tag{$\bar{\boldsymbol y} = 0$} \\
&= E( (\boldsymbol H \boldsymbol x + \boldsymbol z) (\boldsymbol H \boldsymbol x + \boldsymbol z)^H)  \tag{代入} \\
&= E( (\boldsymbol H \boldsymbol x) (\boldsymbol H \boldsymbol x)^H + z z^H)  \tag{$X,Z$统计独立} \\
&= H E(x x^H) H^H + E(z z^H) \\
&= \frac{P_x}{P_z} · \boldsymbol H \boldsymbol Σ_X \boldsymbol H^H + \boldsymbol Σ_Z
\end{align*}
$$
$$
\begin{align*}
\Rightarrow C &= \max_{\boldsymbol Σ_X} 1/2 \log \frac{|\frac{P_x}{P_z} · \boldsymbol H \boldsymbol Σ_X \boldsymbol H^H + \boldsymbol Σ_Z|}{|\boldsymbol Σ_Z|}  \tag{代入} \\
&= \max_{\boldsymbol Σ_X} 1/2 \log |\frac{P_x}{P_z} · \boldsymbol H \boldsymbol Σ_X \boldsymbol H^H + \boldsymbol I_{N_r}|
\end{align*}
$$

- 发送机预编码$V$, 接收机预编码$U^H$, 将$\boldsymbol Σ_X$化为对角阵, 从而使多输入多输出信道化为多个并行的单输入单输出信道.
$$
\begin{align*}
\Rightarrow C &= \max_{P_i} \sum_i^{N_r} \log(1 + \frac{P_i σ_i}{σ_z^2}) \\
& \quad  s.t. \sum_i^{N_r} P_i = P_x
\end{align*}
$$
- 解凸优化问题, 注水原理. 根据实际情景的具体参数, 代回信道容量解出数值结果.
$$
\begin{align*}
P_i^* &= \max\{ 0, \frac{1}{ν^*} - α_i \} \\
\sum P_i &= P_x
\end{align*}
$$

## Problem
### 预编码
发送机预编码$V$, 接收机预编码$U^H$, 将$\boldsymbol Σ_X$化为对角阵, 从而使多输入多输出信道化为多个并行的单输入单输出信道.

### 接收机预编码
$$
\boldsymbol y = \boldsymbol H \boldsymbol x + \boldsymbol z
$$
知$\boldsymbol y, \boldsymbol H$ 求$\boldsymbol x$. 
- 迫零法, 不考虑$z$, 解线性方程
$$
\boldsymbol y = \boldsymbol H \boldsymbol x
$$
知$\boldsymbol y, \boldsymbol H$ 求$\boldsymbol x$. 
Answer
$$
\boldsymbol x_{\text{估计}} = \boldsymbol H^+ \boldsymbol y
$$

- 最小均方误差 (MMSE)
$$
\begin{align*}
\min_{\boldsymbol W} \quad & E(||\boldsymbol W \boldsymbol y - \boldsymbol x||_2^2) 
\end{align*}
$$

Answer
$$
\boldsymbol W = \boldsymbol H^H (\boldsymbol H \boldsymbol H^H + \frac{σ_z^2}{P} \boldsymbol I)^{-1}
$$

- Proof
$$
\begin{align*}
\min_{\boldsymbol W} \quad & E(||\boldsymbol W \boldsymbol y - \boldsymbol x||_2^2) 
\Rightarrow \min_{\boldsymbol W} \quad & E( (\boldsymbol W \boldsymbol y - \boldsymbol x) (\boldsymbol W \boldsymbol y - \boldsymbol x)^H ) 
\end{align*}
$$

$$
\begin{align*}
\Rightarrow E( (\boldsymbol W \boldsymbol y - \boldsymbol x) \boldsymbol y^H ) &= 0
E( \boldsymbol W \boldsymbol y \boldsymbol y^H - \boldsymbol x \boldsymbol y^H ) &= 0
\boldsymbol W E(\boldsymbol y \boldsymbol y^H) &= E(\boldsymbol x \boldsymbol y^H)
\Rightarrow \boldsymbol W &= E(\boldsymbol x \boldsymbol y^H) E(\boldsymbol y \boldsymbol y^H)^{-1}
&= E(\boldsymbol x (\boldsymbol H \boldsymbol x + \boldsymbol z)^H) · E((\boldsymbol H \boldsymbol x + \boldsymbol z) (\boldsymbol H \boldsymbol x + \boldsymbol z)^H)^{-1}  \tag{代入}
&= E( \boldsymbol x \boldsymbol x^H \boldsymbol H^H + \boldsymbol x \boldsymbol z^H) · E(\boldsymbol H \boldsymbol x (\boldsymbol H \boldsymbol x)^H + 2 \boldsymbol z (\boldsymbol H \boldsymbol x)^H + \boldsymbol z \boldsymbol z^H)^{-1}
&= E(\boldsymbol x \boldsymbol x^H) \boldsymbol H^H · (\boldsymbol H E(\boldsymbol x \boldsymbol x^H) \boldsymbol H^H + E(\boldsymbol z \boldsymbol z^H))^{-1}
&= \boldsymbol Σ_X \boldsymbol H^H · (\boldsymbol H \boldsymbol Σ_X \boldsymbol H^H + \boldsymbol Σ_Z)^{-1}
&= P \boldsymbol H^H · (P \boldsymbol H \boldsymbol H^H + σ_z^2 \boldsymbol I)^{-1}
&= \boldsymbol H^H · (\boldsymbol H \boldsymbol H^H + \frac{σ_z^2}{P} \boldsymbol I)^{-1}
\end{align*}
$$

- 混合模数预编码

* 多用户MIMO



# Multi-user MIMO
## 场景
- $N_t$ 个发送天线, 
- $N_u$ 个用户,
- $N_r$ 个接收天线 (每个用户)
-  发送信号 $x = W s$
用户i的接收信号 
$$
y_i = H_i x + n_i  \\
= H_i W s + n_i
$$

$$
\begin{align*}
s \in C^{N_u × 1}  \tag{原始信号}\\
x \in C^{N_t × 1}  \tag{发送信号}\\
y_i \in C^{N_r × 1}  \tag{用户i的接收信号}\\
n_i \in C^{N_r × 1}  \tag{用户i的噪声}\\
W \in C^{N_t × N_u}  \tag{预编码矩阵}\\
H_i \in C^{N_r × N_t}  \tag{信道矩阵}
\end{align*}
$$

### Pre coding (downlink)
- 目的
将多用户之间的干扰消除掉. 前提是发送端知道信道状态信息.
- 非线性预编码
- 脏纸编码
- 迫零脏纸编码
- 串行迫零脏纸编码
- Tomlinson-Harashima 预编码
- Trellis 预编码
- 线性预编码
### Beamforming
$$
x = W s  \tag{发送信号}
$$
波束成形仅仅需要在发送端乘一个线性的波束成形矩阵.
- 随机波束成形
- 迫零波束成形
- MMSE波束成形
- 块对角化预编码
- 预编码矩阵


$$
W_i = V_{i (2)} V'_{i (1)}
$$
其中, 
$V_{i (2)}, V'_{i (1)}$ 来自 
$$
\begin{align*}
\tilde H_i = \left(\begin{matrix} H_1 \\ \vdots \\ H_{i-1} \\ H_{i+1} \\ \vdots \\ H_n \end{matrix}\right)\\
= U_i \left(\begin{matrix} Σ & 0 \\ 0 & 0 \end{matrix}\right) \left(\begin{matrix} V_{i (1)}^H \\ V_{i (2)}^H \end{matrix}\right)  \tag{$V_{i (2)}$}\\
H'_i = H_i V_{i (2)} = U' \left(\begin{matrix} Σ & 0 \\ 0 & 0 \end{matrix}\right) \left(\begin{matrix} V'^H_{i (1)} \\ V'^H_{i (2)} \end{matrix}\right)  \tag{$V'^H_{i (1)}$}
\end{align*}
$$

- 信道容量
$$
C = \sum_i \log |I + \frac{Σ^2 P}{σ_n^2}|
$$
其中, $P$是功率分配的对角矩阵.
- Proof
发送信号, 接收信号,
$$
\begin{align*}
x = \sum_i W_i s_i  \tag{发送信号}\\
y = H_i x + n_i  \tag{接收信号}\\
= H_i \sum_j W_j s_j + n_i\\
= H_i W_i s_i + H_i \sum_{i ≠ j} W_j s_j + n_i 
\end{align*}
$$

目的, 是找到$W_i$使得干扰项归零
$$
\begin{align*}
\left\{\begin{matrix}\\
H_i W_i = I\\
H_j W_j = \boldsymbol 0  &\quad ; i ≠ j\\
\end{matrix}\right.  \tag{干扰项归零}
\end{align*}
$$

即,
$$
\begin{align*}
\left\{\begin{matrix}
\tilde H_i W_i = \boldsymbol 0  &\quad  ...(1)\\
H W = \left(\begin{matrix} H_1 W_1 && \boldsymbol 0\\ & \ddots &\\ \boldsymbol 0 && H_n W_n \end{matrix}\right)  &\quad  ...(2)\\
\end{matrix}\right.
\end{align*}
$$

$$
\begin{align*}
\tilde H_i = \left(\begin{matrix} H_1 \\ \vdots \\ H_{i-1} \\ H_{i+1} \\ \vdots \\ H_n \end{matrix}\right)\\
H = \left(\begin{matrix} H_1 \\ \vdots \\ H_n \end{matrix}\right)\\
W = \left(\begin{matrix} W_1 & ... & W_n \end{matrix}\right)\\
\end{align*}
$$
对于$(1)$, 即$W_i$在$\tilde H_i$的零空间内. 矩阵论有, 矩阵$\tilde H_i$的SVD分解中$V$矩阵的第$r~n$列是其零空间的基向量组 $Null (A) = Span(v_{r+1}, ... , v_n)$. 即, $V_{i (2)}^H$ 满足$(1)$, 可将其作为预编码矩阵的一部分$W_i = V_{i (2)} W_{i (2)}$.
$$
\begin{align*}
\tilde H_i = U_i \left(\begin{matrix} Σ & \boldsymbol 0 \\ \boldsymbol 0 & \boldsymbol 0 \end{matrix}\right) \left(\begin{matrix} V_{i (1)}^H \\ V_{i (2)}^H \end{matrix}\right)\\
H_i V_{i (2)}^H = \boldsymbol 0
\end{align*}
$$
对于$(2)$, 令$H'_i = H_i V_{i (2)}$, 对其SVD分解, 则以$V'^H_{i (1)}$作为预编码矩阵的后部分$W_i = V_{i (2)} V'^H_{i (1)}$, 以$U'_{i (1)}$作为接受端处理矩阵, 则可以满足$(2)$.
$$
\begin{align*}
H_i W_i = H_i V_{i (2)} W_{i (2)}  \tag{代入}\\
= H'_i W_{i (2)}\\
H'_i = \left(\begin{matrix} U'_{i (1)} & U'_{i (2)} \end{matrix}\right) \left(\begin{matrix} Σ & \boldsymbol 0 \\ \boldsymbol 0 & \boldsymbol 0 \end{matrix}\right) \left(\begin{matrix} V'^H_{i (1)} \\ V'^H_{i (2)} \end{matrix}\right)\\
=> U'^H_{i (1)} H'_i V'_{i (1)} = Σ
\end{align*}
$$

综上, 预编码矩阵为 $W_i = V_{i (2)} V'_{i (1)}$

信道容量, 可得
$$
C = \sum_i \log |I + \frac{Σ^2 P}{σ_n^2}|
$$

