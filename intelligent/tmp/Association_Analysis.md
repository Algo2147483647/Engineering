# Association Analysis

[TOC]

## Problem

存在一个0/1表格, 每一行对应一个记录, 每一列对应一个项, 表中每一个0/1值表示该项是否存在于该事物中.

- Itemset: 包含一些项的集合.

- Association Rules
  $$x \to y$$
  其中, $x \cup y = \emptyset$
  关联规则表征两个项之间可能存在很强的关联.

- 度量指标: Support、Confidence
  对于项集$X, Y$
  $$
  \begin{align*}
    support(X \to Y) &= \frac{number(X \cup Y)}{number(T)}  \tag{Support}  \\
    confidence(X \to Y) &= \frac{number(X \cup Y)}{number(X)}  \tag{Support}  \\
    number(X) &= number({t_i | X \subseteq t_i, t_i \in T})
  \end{align*}
  $$

  - Support: 表征数据集中包含该项集的记录所占的比例.
  - $T = \{t_1, ... ,t_N\}$: 所有记录的集合, $t_i$是表格第i行的记录.

- Frequent itemset  
  关联规则的两个项集的并集, 且其关联度大于等于给定的阈值. 即 Frequent itemset表征经常出现在一起的项的集合.

- Problem  
  寻找关联规则, 即关联度、Confidence都大于等于给定的阈值.
  $$
  \begin{align*}
    support(X \to Y) &≥ minsupport  \\
    confidence(X \to Y) &≥ minconfidence
  \end{align*}
  $$


## Property

- 项集频繁, 则其子集频繁$\Leftrightarrow$项集不频繁, 则其超集不频繁.
- 若规则$X \to Y - X$低于Confidence阈值, 则对于$X$子集$X'$, 规则$X' \to Y - X'$也低于Confidence阈值
- Frequent itemset 生成的方法:
  - $F_k = F_{k-1} × F_1$
  - $F_k = F_{k-1} × F_{k-1}$

## Algorithm

### Apriori

Frequent itemset 每一项各不相同,  每一项内部排列有序.

**步骤**

- 对于K = 1 : N项的项集, 迭代
  - Frequent itemset 生成
    对于K项项集
    - Frequent itemset 子集生成. 生成K项所有可以组合的集合. 
      eg.$(frozenset({2, 3}), frozenset({3, 5})) \to (frozenset({2, 3, 5}))$
    - 保存满足Support阈值的集合.
  -  关联规则生成
    对不同长度(K)的Frequent itemset 依次分析
    - Frequent itemset 只有两个元素{AB}, 直接计算ConfidenceP(A→B),P(B→A)
    - Frequent itemset 超过两个元素{ABC...}, 依次计算ConfidenceP(AC...→B)
    - 保存满足目标Confidence的关联规则.
