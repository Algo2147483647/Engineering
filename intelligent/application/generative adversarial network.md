# Generative Adversarial Network

[TOC]

## Architecture

- Generator: The generator's role is to create fake data (e.g., images, audio) from random noise. Its goal is to fool the discriminator into believing the fake data is real.
- Discriminator: The discriminator is a classifier that evaluates whether a given data sample is real (from the training set) or fake (from the generator).

## Train

$$
\begin{align*}
L_G &= -\mathbb{E}_{z \sim p_z(z)}[\log D(G(z))]\\
L_D &= -\mathbb{E}_{x \sim p_{\text{data}}(x)}[\log D(x)] - \mathbb{E}_{z \sim p_z(z)}[\log(1 - D(G(z)))]
\end{align*}
$$

The GAN training process converges to a **Nash equilibrium**, where the generator creates data so realistic that the discriminator cannot distinguish it from real data. At this equilibrium, 

- discriminator has an accuracy of $50\%$ on distinguishing real vs. generated data,  $D(x) = p_{\text{data}}(x) / (p_{\text{data}}(x) + p_{\theta}(x))$
- generator produces samples that lie in the same distribution as the real data distribution.

