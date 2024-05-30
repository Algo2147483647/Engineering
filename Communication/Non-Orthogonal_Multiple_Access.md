# Non-Orthogonal Multiple Access

[TOC]

NOMA allows multiple users to transmit data on the same time and frequency resources without requiring orthogonal signals between them. The core idea of NOMA is to adjust the transmission power and encoding method of each user, so that signals from different users can be separated at the receiving end.

### DownLink

弱用户User1直接解出自己的信号即可, 此时将User2的信号当做干扰. 
强用户User2先解出User1的信号, 然后User2从其接收信号中减去User1的信号, 再解自己的信号. 
$$
\begin{align*}
x = \sum_i \sqrt{α_i P} x_i \quad ;\sum_i α_i = 1  \tag{发送信号}\\
y_i = h_i x + n_i  \tag{用户i接受信号}
\end{align*}
$$
**2个用户模型**

**场景**
$$
\begin{align*}
x &= \sqrt{α P} · x_1 + \sqrt{(1 - α) P} · x_2  \tag{发送信号}\\
y_1 &= h_1 x + n_1  \tag{用户1接受信号}\\
&= h_1 \sqrt{α P} · x_1 + h_1 \sqrt{(1 - α) P} · x_2 + n_1\\
y_2 &= h_2 x + n_2  \tag{用户2接受信号}
\end{align*}
$$
信道容量
$$
\begin{align*}
SINR_1 &= \frac{α P |h_1|^2}{(1-α) P |h_1|^2 + N_1}  \tag{远端用户1信干噪比}\\
SINR_2 &= \frac{(1 - α) P |h_2|^2}{N_2}  \tag{近端用户2信干噪比, 用户1信号被理想删除}\\
C_1 &= \log_2(1 + SINR_1)  \tag{远端用户1信道容量}\\
&= \log_2(1 + \frac{α P |h_1|^2}{(1-α) P |h_1|^2 + N_1})\\
C_2 &= \log_2(1 + SINR_1)  \tag{近端用户2信信道容量}\\
&= \log_2(1 + \frac{(1-α) P |h_2|^2}{N_2})
\end{align*}
$$

## 关键技术

### Superposition coding
### Serial interference cancellation SIC