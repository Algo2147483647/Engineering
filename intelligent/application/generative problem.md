# Generative Problem

[TOC]

## Problem

In a generative problem, the goal is to approximate the true data distribution $p_{\text{data}}(x)$ with a model distribution $p_{\theta}(x)$, where $\theta$ are the parameters of the model. The dataset consists of examples $\{x_1, \cdots, x_n\}$ that are sampled from the true distribution $p_{\text{data}}(x)$.

The generative model describes a distribution $p_{\theta}(x)$ defined implicitly by taking points from a simple prior distribution (such as unit distribution) $p_{prior}(z)$ and mapping them to the complex data space $x$ through a transformation $g_\theta(z)$. 

![gen_models_diag_2](./assets/gen_models_diag_2.svg)

## Solution

<img src="assets/generative-overview.png" alt="img" style="zoom: 18%;" />