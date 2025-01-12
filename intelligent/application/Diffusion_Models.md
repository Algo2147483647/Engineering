# Diffusion Model

[TOC]

1. **扩散过程（正向过程）**：在扩散过程中，模型学习如何逐步加入噪声到数据中。这个过程通常被描述为一系列概率分布$p(x_{t}|x_{t-1})$，其中$x_t$表示在时间步骤$t$的数据状态，而$x_0$是原始数据。对于图像，$x_0$将是一张图片。通常，这些概率分布被选择为高斯分布，即：
   $$
   x_t = \sqrt{1 - \beta_t} x_{t-1} + \sqrt{\beta_t} \epsilon
   $$
   
   > $$
   > \begin{aligned}
   > \mathbf{x}_{t} & =\sqrt{\alpha_{t}} \mathbf{x}_{t-1}+\sqrt{1-\alpha_{t}} \epsilon_{t-1} \\
   > & =\sqrt{\alpha_{t}}\left(\sqrt{\alpha_{t-1}} \mathbf{x}_{t-2}+\sqrt{1-\alpha_{t-1}} \epsilon_{t-2}\right)+\sqrt{1-\alpha_{t}} \epsilon_{t-1} \\
   > & =\sqrt{\alpha_{t} \alpha_{t-1}} \mathbf{x}_{t-2}+\sqrt{{\sqrt{\alpha_{t}-\alpha_{t} \alpha_{t-1}}}^{2}+{\sqrt{1-\alpha_{t}}}^{2}} \bar{\epsilon}_{t-2} \\
   > & =\sqrt{\alpha_{t} \alpha_{t-1}} \mathbf{x}_{t-2}+\sqrt{1-\alpha_{t} \alpha_{t-1}} \bar{\epsilon}_{t-2} \\
   > & =\cdots \\
   > & =\sqrt{\bar{\alpha}_{t}} \mathbf{x}_{0}+\sqrt{1-\bar{\alpha}_{t}} \epsilon
   > \end{aligned}
   > $$
   >
   > 
   
   其中，$\beta_t$是预先定义的噪声水平，$\epsilon$是从标准正态分布中抽取的噪声。
   
2. **逆扩散过程（反向过程）**：在逆扩散过程中，模型学习如何从纯噪声中重构出数据。这个过程可以被看作是一个参数化的马尔可夫链，其目标是学习一个逆过程$q(x_{t-1}|x_t)$，最终能够重构出$x_0$。在训练过程中，我们通常使用变分下界（Evidence Lower BOund, ELBO）来近似逆过程的分布。

   逆过程通常被参数化为：

   $$
   q_\theta(x_{t-1}|x_t) = \mathcal{N}(x_{t-1}; \mu_\theta(x_t, t), \Sigma_\theta(x_t, t))
   $$

   其中$\mu_\theta$和$\Sigma_\theta$是由神经网络（参数为$\theta$）输出的均值和协方差，神经网络的目标是最小化重构出的$x_0$和真实$x_0$之间的差距。

3. **训练**：训练过程涉及优化神经网络参数$\theta$，以最大化数据的似然或等价地最小化ELBO。这个优化通常通过随机梯度下降（SGD）或其变体来完成。训练目标可以表示为：

   $$
   \min_\theta \mathbb{E}_{x_0, \epsilon \sim \mathcal{N}(0,I), t} \left[ \Vert f_\theta(x_t, t) - \epsilon \Vert^2 \right]
   $$

   这里，$f_\theta$是由神经网络参数化的一个函数，它试图预测加入到$x_0$中的噪声。这个公式的目标是使$f_\theta$能够准确预测在每个时间步骤$t$加入的噪声，因为如果能够准确预测噪声，就可以准确地逆转扩散过程。

通过这种方式，扩散模型能够生成与训练数据相似的新样本。在图像生成的上下文中，这意味着模型能够从随机噪声生成高质量的图片。

## Variational Lower Bound

在概率模型和统计学中，变分下界（Variational Lower Bound）是指一个由变分推断（Variational Inference）方法用来近似复杂概率模型中的后验分布的技术。这个方法通常用在贝叶斯推断中，特别是当后验分布难以直接计算时。

在变分推断中，我们使用一个简单的分布（变分分布）来近似我们感兴趣的复杂后验分布。变分下界就是对模型证据（或边际似然）的一个下界，它是由变分分布定义的。

具体来说，考虑一个有参数$\theta$的模型，和观测数据$x$，我们感兴趣的是后验分布$p(\theta|x)$。变分推断通过引入一个简单的变分分布$q_\phi(\theta)$来近似$p(\theta|x)$，这里$\phi$是变分分布的参数。变分下界（ELBO）是由以下不等式给出的：

$$
\log p(x) \geq \mathbb{E}_{q_\phi(\theta)}[\log p(x|\theta)] - \text{KL}(q_\phi(\theta) || p(\theta)) = \text{ELBO}
$$


这里，$\log p(x)$是对数证据（也称为边际似然），$\mathbb{E}_{q_\phi(\theta)}[\log p(x|\theta)]$是在变分分布下的条件对数似然的期望，而$\text{KL}(q_\phi(\theta) || p(\theta))$是变分分布和先验分布之间的Kullback-Leibler散度。ELBO是对数证据的一个下界，因此通过最大化ELBO，我们可以间接地最大化对数证据。

在优化过程中，我们不是直接计算对数证据，而是优化ELBO，这是因为对数证据往往难以直接计算。通过调整变分分布的参数$\phi$，我们可以使变分分布尽可能接近真实的后验分布，从而使ELBO最大化。

在扩散模型的背景下，变分下界用于训练神经网络来近似逆扩散过程，这样可以从噪声数据中重构出有意义的样本。通过最大化变分下界，我们可以改善模型对数据生成过程的学习。