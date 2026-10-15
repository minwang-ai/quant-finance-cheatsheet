
# State Machines  
> Course source: 6.1200J Lecture 04

| Aspects | Explanation | Note|
|:--:|:--|:--|
| **Definition** | a collection of **states** $Q$, a specified **initial state** $q_0 \in Q$, and a set of allowed **transitions** $T$, **for each state**: a (possibly empty) list of **possible transitions** to other states $q \to r$. | If a state has multiple possible transitions, we say the state machine is **non-deterministic**; otherwise, it is **deterministic**.|
| An **execution** of a state machine | a **(in)finite** sequence of states, starting from the initial state, that follows the transition rules, i.e., $q_0 \to q_1 \to q_2 \to \cdots (\to q_n)$, where each $q_i \to q_{i+1} \in T$|

## Reachability and invariants
| Terms/Features | Explanation | Note|
|:--:|:--|:--|
|**Reachability**|A state $r$ is **reachable** if there is some execution that reaches that state $q_0 \to \cdots \to r$| If there is no possible execution, the state is unreachable |
|**Predicate**|$P(q)$ is **true or false** depending on state $q \in Q$| We could think about it as a function from a set of states $Q$ to boolean values $\{\text{true}, \text{false}\}$ |
|**Preserved Predicate** | a predicate $P(\cdot)$ defined on states, such that **the truth of $P(\cdot)$ is preserved along transitions**, i.e., if $P(q)$ is true for a state $q$, and there exists a transition $q \to r \in T$ from $q$ to $r$, then $P(r)$ is true as well. | i.e., $\forall q \to r \in T,\; P(q) \to P(r)$|
| **Invariant** | a property $P(q)$ that is **true for all reachable states**. <br><br>**Proof** by Invariant Principle. Steps:<br>1. Show $P(q_0)$ is true <br>2. Show $P(q)$ is preserved. <br>Consider any $q \to r \in T$, assume $P(q)$ is true, want to show $P(r)$ is true | Theorem - **The Invariant Principle** (generalization of the induction axioms, can be proved by strong induction):<br> Suppose $P(\cdot)$ is **true for the initial state** $q_0$, i.e., $P(q_0)$ is true and is a **preserved predicate**, i.e., $\forall q \to r \in T,\; P(q) \to P(r)$. Then $P(\cdot)$ is an **invariant**. <br><br>Corollary (following the theorem): <br>If $P(r)$ is false and $P(\cdot)$ is an invariant, then state $r$ is **unreachable**|


Example: 8 puzzle

- $P(q)$ = the number of inverted pairs in state $q$ is odd
- $P(q)$ is preserved because
    - Horizontal moves: The order does not change, so P(r) is true    
    - Vertical moves: Consider the sequence $i, j, k, *$. Moving $i$ downwards—swapping $i \leftrightarrow *$—is equivalent to swapping $i \leftrightarrow j$ and then $i \leftrightarrow k$ (two adjacent swaps in reading order). Each swap changes the number of inverted pairs by either $+1$ or $-1$. Therefore, two adjacent swaps change the number of inverted pairs by $(\pm 1) + (\pm 1) = \text{even}$. When $P(q)$ is true, the number of inverted pairs is odd; after this operation, it is still odd, so $P(r)$ remains true.
- Then use invariant principle and Corollary to prove states are reachable or unreachable




## Termination
| Terms/Features | Explanation | Note|
|:--:|:--|:--|
|**final state** | state $q$ with no possible transitions.| no $q \to r \in T$|
| **terminate** definition | if there are **no infinite executions**.|Intuitively, if we try to run the state machine, then no matter what choices we make for **each transition**, we end up at a **final state**. It means the algorithm will not run forever.|
| correct | if the state machine terminates and partially correct |**partially correct** means if the state machine terminates then it gives correct answer|
| **derived variable** (aka potential function) | a function $X(q)$ **mapping states** $Q$ to **real numbers** $\mathbb{R}$, i.e., for each state $q \in Q$, value $X(q) \in \mathbb{R}$| Analog to state predicates: state predicates $P(q)$ map state $Q$ to **boolean values** $\{\text{true}, \text{false}\}$|
|A derived variable $X(q)$ is **strictly decreasing** | if, for any transition $\forall q \to r \in T$, $X(q) < X(r)$. |It is weakly decreasing if $X(q) \le X(r)$.|
| **Termination Theorem** |Suppose $X(q)$ is a derived variable with **natural number** (non-negative integer) values that is **strictly decreasing**. Then we are guaranteed the state machine **terminates**.| i.e., satisfying <br> 1. $X(q) \in \mathbb{N}, \forall q \in Q$ <br>2. $X(q)$ is strictly decreasing <br><br> It can be proved by induction. The idea is that all executions have length $\le X(q_0)$|

Example - simple sort

- Algorithm: while $\exists i,\; a_i > a_{i+1}$, swap $a_i \leftrightarrow a_{i+1}$.
- $X(q)$ is the number of inverted pairs ($a_i > a_j$ where $i < j$) in state $q$, therefore $X(q) \in \mathbb{N}$.
- The state machine terminates because $X(q)$ is strictly decreasing: for transition $q \to r$, $X(r) = X(q)-1$.
