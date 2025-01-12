# Granger Causality

[TOC]

## Define

Granger Causality relationship from time series $Y$ to $X$ based on two principles, to test the null hypothesis that $x$ does not Granger-cause $y$,

- The cause happens prior to its effect.
- The cause has unique information about the future values of its effect.
$$
y_t = a_0 + \sum_{i=1}^m a_i y_{t-i} + \sum_{i=1} b_i x_{t-i} + \epsilon_t
$$

## Property

* Structural Causal Model

## Algorithm

### Transfer Entropy 

**Define**
$$
\begin{align*}
\text{TE}_{X \rightarrow Y} &= I(X_t ; Y_{t-1:t-L} | X_{t-1:t-L})  \\
&= H(X_t | X_{t-1:t-L}) - H(X_t | X_{t-1:t-L}, Y_{t-1:t-L})  \\
&= \sum \mathbb P(x_t, x_{t-1:t-L}, y_{t-1:t-L}) · \log_2 \frac{\mathbb P(x_t | x_{t-1:t-L}, y_{t-1:t-L})}{\mathbb P(x_t | x_{t-1:t-L})}
\end{align*}
$$

Transfer entropy is a non-parametric statistic measuring the amount of directed (time-asymmetric) transfer of information between two random processes $X, Y$.
