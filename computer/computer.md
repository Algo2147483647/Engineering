# Computer

[TOC]

## Mathematical model: Turing Machine

A Turing machine is a mathematical model of computation describing an abstract machine that manipulates symbols on a strip of tape according to a table of rules. Turing machine can be formally defined as a 7-tuple $M = M=\left\langle Q, \Gamma, b, \Sigma, \delta, q_{0}, F\right\rangle$, where

- $\Gamma$ is a finite, non-empty set of tape **alphabet symbols**;
  - $b \in \Gamma$ is the **blank symbol** (the only symbol allowed to occur on the tape infinitely often at any step during the computation);
  - $\Sigma \subseteq \Gamma \backslash\{b\}$ is the set of **input symbols**, that is, the set of symbols allowed to appear in the initial tape contents;
- $Q$ is a finite, non-empty set of **states**;
  - $q_0 \in Q$ is the **initial state**;
  - $F \subseteq Q$ is the set of *final states* or **accepting states**. The initial tape contents is said to be *accepted* by $M$ if it eventually halts in a state from $F$.
- $\delta:(Q \backslash F) \times \Gamma \nrightarrow Q \times \Gamma \times\{L, R\}$ is a partial function called the **transition function**, where $L$ is left shift, $R$ is right shift. If $\delta$ is not defined on the current state and the current tape symbol, then the machine halts; intuitively, the transition function specifies the next state transited from the current state, which symbol to overwrite the current symbol pointed by the head, and the next head movement.

### Halting problem

the halting problem is the problem of determining, from a description of an arbitrary computer program and an input, whether the program will finish running, or continue to run forever.

The halting problem is undecidable, meaning that no general algorithm exists that solves the halting problem for all possible program–input pairs.

## Architecture

### Von Neumann Architecture

<img src="./assets/1024px-Von_Neumann_Architecture.svg.png" alt="undefined" style="zoom:33%;" />

Von Neumann architecture describes a design architecture for an electronic digital computer with these components:

- A processing unit with both an arithmetic logic unit and processor registers
- A control unit that includes an instruction register and a program counter
- Memory that stores data and instructions
- External mass storage
- Input and output mechanisms

### Harvard Architecture

<img src="./assets/1024px-Harvard_architecture.svg.png" alt="undefined" style="zoom:33%;" />





