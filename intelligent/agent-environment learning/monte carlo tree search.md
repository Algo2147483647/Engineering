# Monte Carlo Tree Search

[TOC]

Monte Carlo Tree Search (MCTS) is a tree-based search algorithm that incrementally builds information in the search tree through four key steps: selection, expansion, simulation, and backpropagation. By balancing exploration and exploitation, MCTS progressively converges towards an optimal solution. MCTS efficiently searches without a complete game tree, relying only on simulation to explore possible outcomes, and is suitable for scenarios where the game tree is very large.

**Select**: Starting from the root node, MCTS uses a combination of exploration and exploitation to select the most promising node to expand.

- Exploration: Selecting nodes that have not been visited often. Using Upper Confidence Bound to choose action $A_k$ for state $S_k$.

$$
\begin{align*}
\text{UCD}(S_k) &= \tilde V(S_k) + C \sqrt{\frac{\ln(N_{_\text{visit}}(S_{k-1}))}{N_\text{visit}(S_k)}}  \\
\tilde V(S_k) &= \frac{\sum R_{\text{simulate}}(S_k)}{N_{\text{visit}}(S_k)}
\end{align*}
$$

- Exploitation: Selecting nodes that have led to good results in the past. 

$$
\tilde{S_k^*} = \arg\max_{S_k \in \mathcal S} \tilde V(S_k)
$$

**Expand**: Once a node has been selected for expansion, MCTS adds one or more child nodes to the tree, representing the possible moves that can be made from that state.  

**Simulate**: Randomly select action base on the input state, and simulate the game until the termination state is reached.

**Backpropagation**: The reward obtained from Simulation is backpropagated from the leaf node to root, and each related node is updated.


![img](assets/Phases-of-the-Monte-Carlo-tree-search-algorithm-A-search-tree-rooted-at-the-current.png)