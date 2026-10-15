
# 6.1200J Lecture 01: Predicates, Sets, and Proofs
## Collab policy：

Write solutions **on your own**: 

- don’t look at other solutions (from friends, internet,  OR chatGPT).
- don’t reference communal notes while composing your own proof.  

Why? P vs NP fallacy: understanding someone else’s proof is easier that **piecing together your own argument from scratch**.


## Proofs

Goal: read, write and evaluate proofs.

| Term | Definition | Features | Example | 
|:---:|:---:|:--:|:--:|
|**Proof**| a method to **find out the truth**. | | • Experiments /observations (physics) <br> • Sampling (statistics) <br> • Legal (judge/jury) etc|
|**A mathematical proof** | a verifcation of a **proposition** by a chain of **logical deductions** from a base set of **axioms**. |
| **Proposition** | a statement that is **either True or False**. | |• 2 + 3 = 5 (True) <br> •  2 + 3 = 6 (False) |
| **Predicate**| a **proposition** except that it depends on **variables** |(i.e.,  parametrized proposition, once we know what the variables are, it becomes proposition)|•  $∀n ∈ N, n^2 + n + 41$ is prime (False) |
|**Axioms**| An axiom is a **proposition** that is **assumed to be True**.| Diferent **axioms** might be all valid but contradictory to each other and yield diferent **proofs and theorems**. Anyone who agrees with your axioms must accept **theorems derived from them**.  <br><br> There is **no “correct”** set of axioms, but we would at least: <br> •  A set of axioms is **consistent** if **no** proposition can be **both proved and disproved**.  <br> •  A set of axioms is **complete** if **every** proposition can be **either proved or disproved**.(ture proposition can be proved from axioms) <br>  but **Gödel’s Incompleteness Theorem** shows that we **cannot** get both features: **No** set of axioms is **both complete and consistent**. <br> -> Corollary: Since we cannot get both consistancy and complete, if we want consistency (necessary), then **there are True statements that cannot be proved**! (if we want to prove it, we have to add more axioms, then the bigger set of axioms now has other ture statements that cannot be proved) | •  Given a line  $l$ and a point  $p  \in l$, there is exactly one line through  $p$ parallel to  $l$ (Euclidean parallel postulate).  <br> • ..., there is no line through  $p$ parallel to  $l$. (Spherical Geometry) <br> •  ..., there are infnitely many lines through  $p$ parallel  to  $l$. (Hyperbolic geometr) |

### Combining Propositions 
construct new propositions by combining existing ones via boolean operations.

| Term | Denotation | Definition to be True | Example |
|---|---|--|--|
| **A and B** |  $A \land B$ | both A and B are true
| **A or B** |    $A \lor B$ | at least one of A or B is true <br> (Note: this is inclusive or, meaning it’s also fine for A and B to both be true.)
| **not A** |  $\bar{A}$,    $\lnot A$ | A is false |
| **A XOR B** |  $\oplus$ | one or another, but **no both, no neither** <br> (exclusive OR)| We are friends ($A$). <br>We are strangers ($B$).|
| **A NAND B** | | one or another, neither, but **not And**
| **A implies B** |    $A → B$ or  $A \implies B$|if A then B (obeying a rule). <br> It is **equivalent** to its **contrapositive**, `(not B) implies (not A)` but not equivalent to its converse `B implies A`.  <br> Note:<br> - **No causal** relationship (A causes B). <br> -  **no time involved** (A happened, which later caused B to happen) <br> - **Implication Equivalence**  $P \implies Q \equiv \neg P \lor Q$ <br> - The only way to violate implication (make it false):  $A$ happened, but  $B$ didn't. If the condition never happened, so the implication wasn't violated. |  If I smoke ($A$), then I will get lung cancer ($B$). <br> If I never smoke. I don't get cancer. The implication is not violated. |
| **A iff B**|  $A \iff B$| if and only if. It means A and B are **both true or both false** at the same time, meaning they are expressing the **same condition**. It’s equivalent to `(A implies B) and (B implies A)`|

#### Truth Tables
Note:
**Always** refer to the following **truth tables**.

| A | not A |
|---|---|
| T |  F |
| F | T |

| A | B | A and B | A or B| A XOR B | A NAND B | A implies B|
|---|---|:---:|:---:|:---:|:---:|:---:|
| T | T | T | T | F| F | T |
| T | F | F | T | T| T | **F** |
| F | T | F | T | T| T | **T** |
| F | F | F | F | F| T | T |

## Sets

| Term | Explanations | Examples|
|:---:|:---:|:---:|
| **Defination** | A set is a collection of objects|  $A = \{6, 1, 2, 0\}$|
| **Features** |<br> •  **No duplicate**. <br> • **unordered**: the order of elements doesn’t matter. <br> •  can be **fnite**,  **infnite**, **empty**  $\{\}$,  $\varnothing$ <br> • can contain **other sets as elements** | • so sets that have different order of the same elements or has duplicate elements still means the same set  $\{1, 2, 2, 3\} = \{2, 3, 1\} = \{3, 1, 2\}$. <br> natural numbers  $\mathbb{N} = {0, 1, 2, . . .}$, integers  $\mathbb{Z} = \{. . . , −2, −1, 0, 1, 2, . . .\}$, Rationals $\mathbb{Q}$, Real numbers  $\mathbb{R}$, Complex numbers  $\mathbb{C}$ <br> •  $\{2, \{3,4\}, \varnothing$\}
|**Subset**| Sets can be subsets of each other:  $S \subseteq T$ means  $S$ is the subset of  $T$ - all elements of  $S$ are also elements of  $T$. |A empty set is a subset of every set  $\varnothing \subseteq A$|
| **Set-builder Notation**| use **predicates** after \| to specify a **subset**. (Might also see this with a colon instead of \|) |  $\{n \in\mathbb{N} \| isPrime(n)\} = \{2, 3, 5, 7, 11, . . . , \}$ |


### Combine Sets into Other Sets
Example
$A = \{6, 1, 2, 0\}$
$B = \{2, \{3, 4\}, ∅\}$

| Term | Denotation| Explanations | Examples|
|:---:|:---:|:---:|:---:|
| **Intersection** |  $A \cap B$ | The set of elements that are in **both** set A **and** B|  $A \cap B = \{2\}$|
| **Union**  |  $A \cup  B$| The set of elements that are in A **or** B  |$A \cup B = \{0, 1, 2, 6, \{3, 4\}, \varnothing\}$|
| **Diference** |  $A − B = A \setminus B$| The set of elements **in A** that are **not** in  B|  $A − B = A \setminus B = \{0, 1, 6\}$|

## Tuples
| Term | Explanations | Examples|
|:---:|:---:|:---:|
| **Defination** | A tuple is a ordered lists of objects, written with parentheses $(\text{element1}, \text{element2})$||
| **Features** | <br> •  **could have duplicate**. <br> • **ordered**:order matters <br> •  Union, Interection, etc.,  **don’t make much sense** for ordered tuples. |    $X =  (6, 1, 2, 0) \neq   (6, 1, 2, 0, 0) \neq  (2, 1, 6, 0)$|
