---
layout: page
title: "Exact Path Length Problem(EPL)"
description: ""
header-img: "img/avatar.jpg"
type: "note"
---

## Introduction

>Finding shortest paths in weighted graphs is one of the most central problems in graph algorithms.

### what are the other central problems in graph algorithms?
1. longest path
2. graph coloring
3. *topological sorting*
4. *matching*
5. *maximum flow/min-cut*
6. *minimum spanning tree*
7. *rechability/connectivity*

>This problem has plenty of applications.

### for example, what application?
1. *GPS route planning*
2. *network packet routing*
3. *robot navigation*
4. *logistics*

>This problem has several polynomial time solution algorithms now.

### what are the algorithms?
1. Dijkstra
2. Bellman–Ford
3. Floyd–Warshall
4. DAG shortest-path

>On the other hand, finding the longest path is a NP-complete problem.

### review: what is **NP-complete**?

NP-complete = NP + NP-hard. Where NP means a proposed solution can be verified in a polynomial time, while **NP-hard** means every NP problem can reduce to the NP-hard problem in a polynomial time. i.e. A NP-hard problem is the hardest problem in NP.

### review: what is **reduce**?

Reduce A to B means transform any instance of problem A into B in polynomial time, and preserve the YES/NO answer.

For decision problem $A,B$:

$$
A\le_p B
\iff
\exists f \text{ computable in polynomial time, s.t. }
x\in A \iff f(x)\in B.
$$

$f$ is the **polynomial-time reduction**.

### review: what is **decision problem**?

It is identified with the set of YES-instances.

Example: let **A = Subset Sum**.

$$
A=\{(u_1,\dots,u_m,B):\exists J,\ \sum_{j\in J}u_j=B\}
$$

Take

$$
x=(3,5,8,11).
$$

Since

$$
3+8=11,
$$

we have

$$
x\in A.
$$

---

Instead of finding the shortest path(here the shortest means lowest cost), we ask when given cost k, is there exist a path of cost k?

The weight here are integers. The graph we considered are **directed multi-graph**.

**Definition 1**. Given two nodes p, q ∈ V(G) from G and a target cost k, the exact path length(EPL) problem is to determine whether or not there is a path in G from the initial node p to the final node q with cost exactly k.

```text
Original EPL
(edges may be + / - mixed)
        |
        | sign-relaxation
        v
   unsign(G)
(add shortcut edges)
        |
        | remove sign alternation
        v
Sign-free EPL
(all + or all -)
        |
        | DP / matrix method
        v
 Is there a path of cost k?
      YES / NO
```

For example:

```text
A --(+5)--> B --(-2)--> C

        relaxation
            ↓

A --(+3)--------------> C
```

>The same approach enables us to solve the problem of finding a path with the smallest absolute cost in pseudo-polynomial time between two given nodes. 

### what is the problem of finding a path with the smallest absolute cost?

min abs(cost).

>The motivation for EPL in fact comes from the case when the weights are integer vectors, which comes from the analysis of **multi-tape automata**.

### what is multi-tape automata?

It's an automata modeled with several tapes. Here is the mathematical definition when the weights are trits:

$$
M=(Q,\Sigma_1,\dots,\Sigma_h,\delta,q_0,F)
$$

with transition function

$$
\delta:
Q\times \Sigma_1\times\cdots\times\Sigma_h
\to
Q\times\{-1,0,+1\}^h
$$

Each component of

$$
(-1,0,+1)
$$

means one tape head moves left, stays, or moves right. The machine has finite states and read-only tapes. 

Example: a 2-tape automaton checks whether first symbols match.

$$
Q=\{q_0,q_{yes},q_{no}\}
$$

$$
\delta(q_0,a,a)=(q_{yes},(1,1))
$$

$$
\delta(q_0,a,b)=(q_{no},(1,1))
$$

Each step reads both tapes and moves both heads right. The head of the tape will read the letters, and check the automaton to see how the state will change.

```text
heads read symbols
      ↓
current state + symbols
      ↓
choose a transition
      ↓
change state + move heads
```

### summarizing the motivation:

```text
string database query
        ↓
executed by multi-tape automaton
        ↓
need to know: will it loop forever?
        ↓
look at automaton's transition graph
        ↓
each transition = edge
head movements = vector weight
        ↓
a loop with total weight (0,...,0)
means heads return to original positions
        ↓
therefore need to detect a path/cycle
with an exact vector cost
        ↓
Exact Path Length problem
```

# Not Arranged

## 2 Pseudo-polynomial time algorithm

### EPL is NP hard

The problem is NP-hard in case all weights are non-negative integers

1. subset sum problem is NP-complete
2. mapping reduction from subset sum problem to EPL problem

### sign relaxation

sign-relaxation of a graph G is another graph with specific properties: they share the same vertex set, and for every path in G, H has a path with same nodes, cost, and also the sgn of each edge in the correspongding path in H are identical, with the sgn of the total cost of this path.

But to get the sign-relaxation, the algorithm must not be polynomial time unless P = NP.

But there still a way to get H, the sign-relaxation. sign-closure. the algorithm is Pseudo-polynomial.

unsign(G) is a sign-relaxation of G.

Summary: construction based.

### solving EPL

When restrict the weights in trits...

then solve the case with maximum absolute weight W, give the time and space complexity.

### Minimum Absolute Cost Path

give the complexity of MAC problem.

---

the way we used to solve EPL also can be used to solve MAC.



## 3 extension to high-dim weight

In this case, EPL is NP-complete.

## the art of writting

First giving the general or somehow visual description to make it easier to understand. Then give a formal definition.

An addition to the previous classical problem. motivation.

## extending

if such path exist, how to find the shortest and longest path? And also the complexity of finding them.