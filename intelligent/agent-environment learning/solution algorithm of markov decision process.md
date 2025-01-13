# Solving Algorithm of Markov Decision Process

[TOC]

## Value-Based methods: Estimate the Value function

For a Markov decision process, the value-based methods is to find the optimal policy indirectly by estimating the value function $V_\pi(s)$ of the policy $\pi$ of each state or state-action pair.

### Dynamic Programming: Iterative search for fixed points

$$
\begin{align*}
\hat V(s) &\leftarrow \max_{a \in A(s)} \left( R(s, a) + \gamma \sum_{s' \in S} \mathbb P(s' | s, a) \hat V(s') \right)  \tag{value iteration}\\
V^{\pi}(s) &= R(s, \pi(s)) + \gamma \sum_{s' \in S} \mathbb P(s' | s, \pi(s)) V^{\pi}(s')\\
\pi'(s) &= \arg \max_{a \in A(s)} \left( R(s, a) + \gamma \sum_{s' \in S} \mathbb P(s' | s, a) V^{\pi}(s') \right)
\end{align*}
$$

Dynamic programming (DP) is an optimization method that decomposes complex problems into simple sub-problems, suitable for decision-making problems with overlapping sub-problems and optimal sub-structures. Dynamic programming updates the state-value function V(s) through value iterati

on or policy iteration to ultimately obtain an optimal strategy.

- Value Iteration: The value functions are updated iteratively until they converge to the optimal value function. Its convergence can be guaranteed by the Bellman optimality equation. Specifically, value iteration start with an initial guess $\hat V^{(0)}(s)$ and the iteration stops when $|\hat V^{\text{new}}(s) - \hat V^{\text{old}}(s)| < \epsilon, \forall s \in S$.
- Policy Iteration: The optimal strategy is gradually approached by alternating strategy evaluation and strategy improvement.

### Monte Carlo Method: Random sampling estimation

$$
V_\pi (s) = \mathbb E \left(\sum_{t=0}^T \gamma^t R_t \ |\ S_0 = s, \pi \right)
$$

Monte Carlo method is used to estimate statistical distributions through large-scale random sampling, without knowing environmental information such as the transition probability $\mathbb P(s', r | s, a)$. Specifically, we randomly sample a large number of complete paths $\left\{G_{\pi, s}^{(1)}, G_{\pi, s}^{(2)}, \cdots \right\}$ starting from state $s$ and then calculate their expectations to estimate the value function $V_\pi(s)$ of following policy $\pi$.
$$
\hat V_\pi(s) \gets \hat V_\pi(s) + \alpha \left(G_{\pi, s}^{(i)} - \hat V_\pi(s)\right)  \tag{sequential update}
$$

In the specific implementation, the sequential update method can be used. 

- $\hat V_\pi(s)$: estimation of the value function.
- $G_t$: the cumulative reward sample value after a complete sampling from state $s$ to the termination.
- $\alpha$: learning rate, controls how much new information updates the current estimate.

### Temporal Difference Learning

$$
\begin{align*}
V_\pi(s)  &\gets V_\pi(s) + \alpha (r + \gamma V_\pi(s') - V_\pi(s))  \\
Q(s, a) &\gets Q(s, a) + \alpha (r + \gamma Q(s', a') - Q(s, a))  \tag{on policy}\\
Q(s, a) &\gets Q(s, a) + \alpha \left(r + \gamma · \max_{a_i' \in A} Q(s', a_i') - Q(s, a)\right)  \tag{off policy}
\end{align*}
$$

Temporal Difference Learning updates the value function at each time step based on partial information. TD learning allowing for immediate feedback without needing to estimate the value function at the end of a complete path like Monte Carlo sampling.

- On-policy:
- Off-policy: 

#### Q-Learning & State-action-reward-state-action

$$
Q(s_t, a_t) \leftarrow Q(s_t, a_t) + \alpha [r_{t+1} + \gamma \max_{a} Q(s_{t+1}, a) - Q(s_t, a_t)]
$$

$$
Q(s_t, a_t) \leftarrow Q(s_t, a_t) + \alpha [r_{t+1} + \gamma Q(s_{t+1}, a_{t+1}) - Q(s_t, a_t)]
$$

State-Action-Reward-State-Action (SARSA) is an on-policy learner.

#### Deep Q-Networks: Q-Learning + Neural networks

Instead of using a Q-table, DQN employs a neural network to approximate the Q-function.

## Policy-Based methods: Direct search the optimal policy

Policy-Based methods directly learn a policy and optimize the policy itself. Specifically, they estimate the probability distribution of selecting a particular action given a state.

### Policy Gradient Ascent Method

原理: 通过策略梯度上升更新随机性策略的参数$\theta$. $J(\theta)$是对策略的性能度量函数, 可定义为$J(\theta) = V_{\pi_\theta} (s_{t=0})$.
$$
\begin{align*}
\mathbb P_\pi (a | s, \theta)  \\
\theta_{t+1} = \theta_{t+1} + \alpha \widehat{\nabla J(\theta_t)}
\end{align*}
$$

Strategy gradient theorem  
$$
\begin{align*}
\nabla J(\boldsymbol \theta) &= \nabla_\theta V(s)  \\
&\propto \sum_{s' \in S} \mathbb P_{μ,\pi}(s') \sum_{a \in A} Q_\pi(s', a) \nabla_\theta \mathbb P_\pi(a | s', \boldsymbol \theta)   \\
&\propto \mathbb E_{s' \sim \mathbb P_{μ,\pi}, a \sim \pi}(Q_\pi(s', a) \nabla_\theta \ln \mathbb P_\pi (a | s'))
\end{align*}
$$

### Policy Gradient

## Comprehensive methods

### Actor-Critic

The Actor-Critic algorithm is a foundational approach that combines the policy-based and value-based methods. It involves two main components

1. **Actor**: This part of the algorithm proposes actions given the current state. The actor is essentially the policy $\pi(a|s)$ of the agent, which can be either deterministic or stochastic. It's responsible for the actual decision-making process.

2. **Critic**: The critic evaluates the actions taken by the actor by computing the value function $V(s)$ or the action-value function $Q(s, a)$. The critic assesses the quality of the actions given the state of the environment.

<img src="assets/R.png" alt="R" style="zoom: 80%;" />

- **Policy (Actor) Improvement**: The actor adjusts its policy parameters $\theta$ based on the gradient of expected rewards. It tries to maximize the expected return by considering the feedback from the critic.

- **Value Function (Critic) Estimation**: The critic updates the value function parameters $w$ to more accurately predict the expected return. The difference between the predicted return and the actual return (the temporal difference error, $\delta$) is used to improve the policy.

- **Temporal Difference (TD) Error**: This is a key concept in actor-critic algorithms. The TD error $\delta$ is calculated by the critic and represents the difference between the predicted reward from the current state-action pair and the reward received plus the predicted reward from the next state. The TD error is then used to update both the actor and the critic.

- **Advantages**: Actor-critic methods aim to combine the advantages of both policy-based and value-based approaches. The critic's value function helps reduce the variance of the policy gradient, leading to more stable and efficient learning than policy-based methods alone. At the same time, because the actor maintains an explicit policy, it can be easier to learn and more effective in high-dimensional or continuous action spaces compared to value-based methods.

- **Variants**: There are many variants of the actor-critic algorithm, including A3C (Asynchronous Advantage Actor-Critic), A2C (Advantage Actor-Critic), and SAC (Soft Actor-Critic), each with its own improvements and optimizations for different scenarios.

### Deep Deterministic Policy Gradient (DDPG)

DDPG is a model-free, off-policy actor-critic algorithm that specifically addresses environments with continuous action spaces.

<img src="assets/Deep-Deterministic-Policy-Gradient-DDPG-algorithm-structure.png" alt="Deep Deterministic Policy Gradient (DDPG) algorithm structure ..." style="zoom: 60%;" />

### Asynchronous Advantage Actor-Critic (A3C)
