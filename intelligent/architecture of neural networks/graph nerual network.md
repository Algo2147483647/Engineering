# Graph Neural Network

[TOC]

## Architecture

Graph neural networks are neural networks designed to work on graph-structured data. GNN is to learn the representation of nodes, edges, and the entire graph by propagating information in the graph. It is based on a recursive message passing mechanism that allows each node to update its own representation through the information of its neighbors.

- Message Passing: Each node exchanges information with its neighbors.
- Aggregation: A node aggregates the information received from its neighbors.
- Update: A node updates its representation based on the aggregated information.

## Graph Convolutional Network

### Architecture

$$
\begin{align*}
  H_{l+1} 
  &= f(H_l, A)   \tag{l$^{th}$ NN layer}\\
  &= \sigma(\tilde A H_l W_l^T)  \\
  H_{out} 
  &= f(X, A)   \tag{the whole NN}\\
  &= \text{softmax}(\tilde A\ \text{ReLU}(\tilde A X W_{(0)}^T) W_{(1)}^T)\\
  \tilde A &= \tilde D^{1/2}\ (A + I_N)\ \tilde D^{-1/2}\\
  \tilde D_{ii} &= \sum_j (A + I_N)_{ij} 
\end{align*}
$$

Graph Convolutional Networks (GCNs) iteratively aggregate and transform feature information from a node’s local neighborhood to learn meaningful node or graph-level representations. GCNs are typically stacked in multiple layers to capture information from larger neighborhoods. Specifically, GCNs determines the neighbor range of each node by normalizing the adjacency matrix $\tilde A$, performs weighted summation (aggregation) of the neighbor features of each node $\tilde A H$, and then extracts new features through neural network operations $\sigma(\cdot W^T)$.

However, as the number of network layers increases, the difference in local information is gradually eliminated due to excessive diffusion of information, and the node features will gradually become similar (over-smooth) over the entire graph and converge to a approximately constant value.

- $G$: Graph
- $N$: number of nodes
- $F_{in}$: number of features per node
- $F_{out}$: number of output features per node
- $X \in \mathbb R^{N×F_{in}}$: feature matrix ; $x_i$ is a feature description for node $i$: 
- $A \in \mathbb R^{N×N}$: adjacency matrix of the Graph $G$
- $H_{out} \in \mathbb R^{N×F_{out}}$: output matrix
- $H_l \in \mathbb R^{N×F_{l}}$: the input of $l^{th}$ neural network layer|
- $W_l \in \mathbb R^{F_{l+1}×F_{l}}$: the wights of $l^{th}$ neural network layer
- $H_{l+1} = f(H_l, A)$: $l^{th}$ neural network layer ; $H_0 = X, H_L = H_{out}$
- $\tilde D$: diagonal node degree matrix of $(A + I_N)$
- $A + I_N$: The adjacency matrix is expanded to a self-loop adjacency matrix by adding the identity matrix $I_N), ensuring that the node's own features are also involved in the aggregation.
- $\tilde D^{1/2} (A + I_N) \tilde D^{-1/2}$: Normalized adjacency matrix of a graph. 

## Graph Attention Network

### Architecture

$$
\begin{align*}
H_{l+1} &= \sigma\left(A H_l W^T\right)   \tag{layer of NN}\\
h_i &= \sigma\left(\sum_{j \in N_i} \alpha_{ij} W h_j\right)  \tag{component formula} \\
\Rightarrow h_i &= \underset{k}{\|} \sigma\left(\sum_{j \in N_i} \alpha_{ij,k} W_k h_j\right)  \tag{multi-head attention}\\
&= \sigma\left(\frac{1}{K} \sum_{k=1}^K \sum_{j \in N_i} \alpha_{ij,k} W_k h_j\right)
\end{align*}
$$

$$
\begin{align*}
  \alpha_{ij} 
  &= \text{softmax}(e_{ij})  \tag{Attention Wights}\\
  &= \text{softmax}(a(W h_i, W h_j))  \\
  &= \text{softmax}(\text{LeakyReLU}(\boldsymbol a^T (W h_i\ ||\ W h_j)))  \\
\end{align*}
$$

Graph attention network computes a learnable attention coefficient $\alpha_{ij}$ for each neighbor based on their features, indicating the importance of the neighbor to the node information. GAT's attention mechanism naturally supports heterogeneous graphs and does not require the global structural information of the graph, but only relies on the characteristics of local neighbors.

- $G$: Graph
- $N$: number of nodes
- $F_{in}$: number of features per node
- $F_{out}$: number of output features per node
- $X \in \mathbb R^{N \times F_{int}}$: input
- $H_{out} \in \mathbb R^{N \times F_{out}}$: output
- $H_{l} \in \mathbb R^{N \times F_{l}}$: input of every layer of NN
- $W_{l} \in \mathbb R^{F_{l+1} \times F_{l}}$: Wights of every layer of NN
- $A_{l} \in \mathbb R^{N \times N}$: Attention Wights of every layer of NN3
- $\alpha_{ij,l} \in \mathbb R$: the Attention Wights of edge $ij$ of every layer of NN
- $\boldsymbol a \in \mathbb R^{2 F_{l+1}}$ is a weight vector
- $||$: denotes concatenation.