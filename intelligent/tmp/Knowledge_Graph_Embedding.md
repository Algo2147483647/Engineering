# Knowledge Graph Embedding

[TOC]

## Purpose

The Purpose of Knowledge graph representation is to learn a mapping to a continuous vector space $f: E \to R^d$ from the knowledge graph $G$ and the relation triples $T$ representing the fact that there is a relation $r_{ij}$ between entities $e_i$ and $e_j$ in the knowledge graph. Where, $d$ is the embedding dimension, 
$$
G = (E, R, T)  \tag{Knowledge Graph}
$$
$$
T = \{(e_i, r_{ij}, e_j) \ |\ e_i, e_j \in E, r_{ij} \in R\}  \tag{relation triples}
$$

## Propose

- The training process is divided into two steps:
  - Generation of positive sample triplets: Randomly select some triplets $(h, r, t)$ from the knowledge graph as positive samples.
  - Generation of negative sample triplets: For each positive sample $(h, r, t)$, randomly replace one of the entities to obtain a negative sample $(h', r, t)$, where $h' \neq h$ or $t' \neq t$.
  - Definition of loss function: For each positive sample $(h, r, t)$ and its corresponding negative sample $(h', r, t)$, define the loss function as:

## Algorithm

### TransE

- Paper  
  *Translating Embeddings for Modeling Multi-relational Data* (2013, Bordes et al.)
- Process
  $$
  f_r(h, t) = \|h + r - t\|_2^
  2$$  

### TransH

- Paper  
  *Knowledge Graph Embedding by Translating on Hyperplanes.* (2014, Wang et al.)
- Process  
  TransH does this by introducing hyperplanes for each relation, which are used to project the entity embedding onto a relation-specific subspace.  
  $$
  f_r(h, t) = \|h_\bot + r - t_\bot\|_2^2
  $$

### TransR

- Paper  
  *Learning Entity and Relation Embeddings for Knowledge Graph Completion*  
- Process  
  TransR learns to map entities and relations into separate vector spaces. TransR models entities and relations in distinct spaces include entity space and relation spaces.
  $$
  f_r(h, t) =  \|h M_r + r - t M_r\|_2^2
  $$
  $$
  L = \sum_{(h, r, t) \in S} \sum_{(h', r, t') \in S'} \max(0, f_r(h, t) + \gamma - f_r(h', t'))
  $$

* RotatE