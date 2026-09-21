# 6.006 Lecture 1: Introduction
## Goal
**solve** computation problems, and **communicate** that our solutions are **correct** and **efficient**.   
 
| Term | Definition | Requirements | Example | 
|---|---|--|--|
|Define a **Problem**| A mapping (binary relation) from problem **inputs** to **correct outputs**. | <br> - Usually **don’t** specify every correct output for all inputs (too many examples; one input could map to many output)  <br> - Provide a verifiable **predicate** (a property) that correct outputs must satisfy (so we can check whether the output is correct or not given a input-output pair)  <br> - **general** problem for **arbitrarily large input size** |  - Not general: small input instance: In this room, is there a pair of students with same birthday?   <br> - General: arbitrarily large inputs: Given any set of n students, is there a pair of students with same birthday? (include year, date, hour, etc.)|
|Design **Algorithms** | a sequence of **procedure** to **map** each input to a **single** **correct** output (**deterministic function**) | | to solve birthday matching:  <br> – Maintain a record of names and birthdays (initially empty)  <br>  – Interview each student in some order   - If birthday exists in record, return found pair. Else add name and birthday to record  <br> – Return None if last student interviewed without success |  
|Prove **Correctness**| - For small inputs: can use case analysis  <br>  - For arbitrarily large inputs, algorithm must be recursive or loop in some way  <br> - Must use **induction** (recursion is such a key concept in computer science) | | Proof of correctness of birthday matching algorithm  
---



*Figure: Problem defination:*
mapping (binary relation, a bipartite graph) from problem **inputs** to **correct outputs**. 
![a bipartite graph](figures/dsa-problem-def.jpeg)
