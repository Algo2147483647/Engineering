## Compressed Sensing

稀疏表达的意义在于降维。且这个降维并不局限于节省空间。更多地意义在于，在Machine Learning，Signal/Image Processing等众多领域，很多反问题(Inverse Problem)都是不适定/病态的(under-determined, ill-posed)。
$$
y = A x + ε, x \in R^n , A: R^n \to R^m, y \in R^m, m < n
$$
为了能获得比较好的解，人们需要x的先验知识。而稀疏性便是众多先验知识中，最为主要的一种。这种降维主要表现于虽然原始信号x的维度很高，但实际的有效信息集中在一个低维的空间里。这种性质使得不适定的问题变得适定(well-posed)，进而获得“好的解”成为可能。
Candes和Tao的文章就信号的稀疏性和1-范数之间的关系给出了明确地定理。一个很粗略的解释如下: 设一个N维信号的稀疏度为k (k << N)(非零元素位置与幅值未知)，对其进行m采样(m < N)，如果m和k之间满足一定的关系，那么通过最小化1-范数可以精确恢复原信号。

稀疏表示

压缩重建
- 稀疏, 维度中大部分元素为零，只有少量的非零元。
- 使用少量基本信号的线性组合表示某一目标信号，称为信号的稀疏表示；
- 用低维的采样数据向量回复或重构Nyquist速率采样的高维数据向量，称为压缩感知。


$$
\boldsymbol A \boldsymbol x = \boldsymbol b
$$
$$
A \in \mathbb C^{m\times n}, \boldsymbol x \in \mathbb C^n, \boldsymbol b \in \mathbb C^m, m << n
$$

## Problem
$$
\min_{\boldsymbol x} \quad & ||\boldsymbol x||_0 = number(x_i ≠ 0 |_{i=1:n})\\
s.t. \quad & \boldsymbol A \boldsymbol x = \boldsymbol b
$$
$$
A \in \mathbb C^{m\times n}, \boldsymbol x \in \mathbb C^n, \boldsymbol b \in \mathbb C^m, m << n
$$
求有无穷多解的线性方程问题.

简化
L0范数非凸且问题为NP-hard, 通过转换为L1范数问题, 将问题简化:
$$
\min_{\boldsymbol x} \quad & ||\boldsymbol x||_1 = \sum_{i=1}^n |x_i|\\
s.t. \quad & \boldsymbol A \boldsymbol x = \boldsymbol b
$$

## Property

- 有限等距性质
$$
(1 - \delta) ||\boldsymbol x|| ≤ ||\boldsymbol A \boldsymbol x|| ≤ (1 + \delta) ||\boldsymbol x||
$$

## Algorithm
### Orthogonal Matching Pursuit
每次迭代选取一个与信号最匹配的解来逐步逼近原始信号，并计算信号的残差，然后从残差中找出最优的解。

$$
\begin{align*}
\boldsymbol A &= (\boldsymbol a_1, ..., \boldsymbol a_n)\\
\hat{\boldsymbol A} &= (\frac{\boldsymbol a_1}{||\boldsymbol a_1||}, ..., \frac{\boldsymbol a_n}{||\boldsymbol a_n||})
\end{align*}
$$
$$
\boldsymbol w = \boldsymbol A^T \boldsymbol b = \left(\begin{matrix} \hat{\boldsymbol a_1}^T \boldsymbol b \\ \vdots \\ \hat{\boldsymbol a_n}^T \boldsymbol b \end{matrix}\right)
$$
**步骤**

- 初始化
$$
\begin{align*}
\boldsymbol r_0 &\gets \boldsymbol b\\
Λ_0 &\gets \emptyset \\
\boldsymbol x_0 &\gets \boldsymbol 0_{n}
\end{align*}
$$
- 迭代
$$
for\ k \gets 1:s
$$
- 计算贡献度，并找到贡献最大的基向量，
$$
Λ_k = Λ_{k-1} \cap \{ \arg\max_{i \in 1:n, i \notin Λ_{k-1}} |\boldsymbol a_i^T \boldsymbol r_{k-1}| \}
$$
$$
\boldsymbol A_k = \boldsymbol A_{Λ_k}
$$

- 计算残差, 最小均方误差

$$
\begin{align*}
\boldsymbol x_k(i \in Λ_k) &\gets \arg\min_{\boldsymbol x} ||\boldsymbol A_k \boldsymbol x - \boldsymbol b||_2 = \boldsymbol A_k^+ \boldsymbol b\\
\boldsymbol x_k(i \notin Λ_k) &\gets 0\\
\boldsymbol r_k &\gets \boldsymbol b - \boldsymbol A \boldsymbol x_k
\end{align*}
$$

