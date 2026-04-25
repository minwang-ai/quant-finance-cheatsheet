
## Proofs
goal: read, write and evaluate proofs.
| Term | Definition  | Example | 
|---|---|--|
|proof| a method to find out the truth.  | • Experiments /observations (physics) <br> • Sampling (statistics) <br> • Legal (judge/jury) etc|
|A mathematical proof | a verifcation of a **proposition** by a chain of **logical deductions** from a base set of **axioms**. |
| **proposition** | a statement that is either True or False. | • 2 + 3 = 5 (True) <br> •  2 + 3 = 6 (False) <br>  • $∀n ∈ N, n^2 + n + 41$ is prime (False)|
| **predicate**| a **proposition** except that it depends on **variables** (parametrized proposition, once we know what the variables are, it becomes proposition)| 


### Combining Propositions
construct new propositions by combining existing ones

| Term | Denotation | Definition to be true |
|---|---|--|
| A and B | A ∧ B | both A and B are true
| A or B |  A ∨ B | at least one of A or B is true <br> (Note: this is inclusive or, meaning it’s also fine for A and B to both be true.)
| not A | $\bar{A}$,  $¬A$ | A is false |
| A XOR B | | no both, no neither <br>(exclusive OR)|
|A NAND B | | not And
|A implies B |  $A → B$ or $A ⇒ B$|if A then B|
---
Note:
When written in formulas, always refer to the following truth tables.
#### truth tables
| A | not A |
|---|---|
| T |  F |
| F | T |
---

| A | B | A and B | A or B| A XOR B | A NAND B | A implies B|
|---|---|:---:|:---:|:---:|:---:|:---:|
| T | T | T | T | F| F | T |
| T | F | F | T | T| T | F |
| F | T | F | T | T| T | T |
| F | F | F | F | F| T | T |
---