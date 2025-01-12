# Minimax algorithm

[TOC]

$$
a_{t}^* = \left\{\begin{matrix} 
\arg\max\limits_{a \in A_t}\ \  V(s_{t}) & \text{for maximizer} \\
\arg\min\limits_{a \in A_t}\ \  V(s_{t}) & \text{for minimizer} 
\end{matrix}\right.
$$

In a two-player, zero-sum game, play alternates between two players, called the maximizer (at the root), and the minimizer as the opponent. Minimax algorithm traverse the decision tree by depth-first search to determine the optimal action $a^*$ for the current player at the root of the game tree.

<img src="./assets/AB_pruning.svg" alt="AB_pruning" style="zoom:40%;" />

### $\alpha \text{-} \beta$ Prune


$$
\left\{\begin{matrix} 
\tilde v_k \le v_k^* & \Rightarrow \tilde v_k \nearrow & \text{for maximizer} \\
\tilde v_k \ge v_k^* & \Rightarrow \tilde v_k \searrow & \text{for minimizer} 
\end{matrix}\right. \Rightarrow \left\{\begin{matrix} 
\tilde v_k \text{update } \Rightarrow \tilde v_k < v_{\text{new\ sampling}}& \text{for maximizer}   \\
\tilde v_k \text{update } \Rightarrow \tilde v_k > v_{\text{new\ sampling}} & \text{for minimizer} 
\end{matrix}\right.
$$

$$
\begin{align*}
\alpha_0 &\gets +\infty \tag{Initial}\\
\beta_0 &\gets -\infty  \\
\alpha_k &\gets \alpha_{k-1}  \\
\beta_k &\gets \beta_{k-1}  \\
\alpha_k &< \alpha_{k-i} \quad, i \in 1: k \tag{Constraint}\\
\beta_k &> \beta_{k-i} \quad, i \in 1: k  \\
\alpha_k &\gets \tilde v_k \quad \text{for maximizer}  \tag{Update}\\
\beta_k &\gets \tilde v_k \quad \text{for minimizer} 
\end{align*}
$$

If $\alpha_k < \beta_k$, there is no possiable acceptable evaluaion value for this state, and we can directly exit the search.

- $\tilde v_k$: is estimated value of the optimal $v_k^* = \max\limits_{a \in A_k}/\min\limits_{a \in A_k}\ V(s_{k})$.
- $\alpha$ is the upper bound of the range of possible adoption of the evaluation value. $\alpha$ represent the best evaluation value of maximizer.
- $\beta$ is the lower bound of the range of possible adoption of the evaluation value. $\beta$ represent the best evaluation value of the minimizer.
