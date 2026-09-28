# 6.006 Lecture 1: Introduction
## Goal
**solve** computation problems, and **communicate** that our solutions are **correct** and **efficient**.   
 
| Term | Definition | Requirements | Example | 
|:---:|:---|:--|:--|
|Define a **Problem**| A mapping (binary relation) from problem **inputs** to **correct outputs**. | <br> - Usually **don’t** specify every correct output for all inputs (too many examples; one input could map to many output)  <br> - Provide a verifiable **predicate** (a property) that correct outputs must satisfy (so we can check whether the output is correct or not given a input-output pair)  <br> - **general** problem for **arbitrarily large input size** |  - Not general: small input instance: In this room, is there a pair of students with same birthday?   <br> - General: arbitrarily large inputs: Given any set of n students, is there a pair of students with same birthday? (include year, date, hour, etc.)|
|Design **Algorithms** | a sequence of **procedure** to **map** each input to a **single** **correct** output (**deterministic function**) | | to solve birthday matching:  <br> – Maintain a record of names and birthdays (initially empty)  <br>  – Interview each student in some order   - If birthday exists in record, return found pair. Else add name and birthday to record  <br> – Return None if last student interviewed without success |  
|Prove **Correctness**|| - For small inputs: can use case analysis  <br>  - For **arbitrarily large inputs**, algorithm must use **induction** (**recursion** is such a key concept) | Proof of correctness of birthday matching algorithm: <br> - **Induct** on $n$: the number of students in record <br>  – **Hypothesis:** if first $n$ contain match, returns match before interviewing student $n + 1$ <br> – **Base case:** $n = 0,$ first $0$ contains no match <br>  – **Inductive steps:** Assume for induction hypothesis holds for $k$, and consider $k + 1$.<br> Two cases: 1. If first $k$ contains a match, already returned a match by induction. 2. Else first $k$ do not have match, so if first $k+1$ has match, match contains the $k+1$ student <br> – Then algorithm checks directly whether birthday of student $k+1$ exists in first $k$  |
|**Communicate Efficiency**| Measure **the number of operations** instead of time, so that the performance of algorithms depend on the **the size of input** instead of underlying machine.|**Asymptotic Notation:** ignore constant factors and low order terms   <br> – upper bounds $O$<br> - lower bounds $\Omega$ <br> - tight bounds (both upper and lower) $\Theta$  <br> <br> **Efficient** if returns in **polynomial time** with respect to input (**not exponential**)| 
--- 



*Figure: **Problem defination:***
mapping (binary relation, a bipartite graph) from problem **inputs** to **correct outputs**. 
![a bipartite graph](figures/dsa-problem-def.jpeg)


*Figure: Complexity:*
$O(1)<O(\log n)<O(n^{1/2})<O(n)<O(n \log n)<O(n^2)<O(2^n)<O(n!)$
![a bipartite graph](figures/complexity_fig.png)

*Table: Complexity:*
![a bipartite graph](figures/complexity_table.png)

### Model of Computation : Word-RAM
| Aspects | Definition | Details|
|:---:|:---|:---|
| **Why do we need it**| Basis for computing efficiency: Specification for **what operations** on the machine can be performed in **constant O(1) time**  | CPU supports constant time operations on a O(1) number of words (**integers**):<br> – **integer** arithmetic: +, -, *, //, % <br> – **logical** operators: &&, \|\|, !, ==, <, >, <=, =>  <br> – **bitwise** arithmetic: &, \|, <<, >>, ...) <br> – Given word $a$, can **read / write** at address $a$||
| **Computation model**| CPU address a consecutive chunk of memory ($w$ bit RAM) in constant time.  (Here the chunk size is called the **word size**, denoted by $w$). $w$-bit word can address $2^w$ addresses in memory| To address largest memory address $\log_2^n$: Require at least $w > \log_2^n$ bits. To address more memory (for arbitrary large input), we need to increase RAM size.|
---

## Data Structure 
| Term | Definition| Example |
|:--:|:---|:--|         
| **data structure** | a way to **store non-constant data**, that supports a set of **operations** (called **interface**)|
| **interface** | A collection of operations|- **Sequence**: Extrinsic order to items (first, last, nth) <br>– **Set**: Intrinsic order to items (queries based on item keys)|
| **Features** | Data structures may implement the **same interface** (**different operations**) with **different performance** | Static Array - fixed width slots, fixed length, static sequence interface: <br>– `StaticArray(n)`: allocate static array of size $n$ initialized to $0$ in $Θ(n)$ time <br>– `StaticArray.get at(i)`: return word stored at array index $i$ in $Θ(1)$ time <br> – `StaticArray.set at(i, x)`: write word $x$ to array index $i$ in $Θ(1)$ time |
---


## How to Solve an Algorithms Problem
| Methods | Details |
|:--:|:---|
| Reduce to a problem you **already know** <br> (use data structure or algorithm) | • Search Problem (Data Structures) <br> • Sort Algorithms <br>•  Shortest Path Algorithms 
| Design your **own (recursive) algorithm** | • Brute Force <br>• Decrease and Conquer <br>• Divide and Conquer <br>• Dynamic Programming (L15-L19) <br>• Greedy / Incremental
---