## core problem

Given a graph and two nodes then finding the shortest path in a weighted graph.

-> what application?

longest -> NP-complete

==> instead of finding the shortest path, we ask when given cost, is there exist a path of cost k?

the weight here are integers. The graph we considered are directed multi.

1. EPL is NP hard. 
2. pseudo-polynomial time algorithm
3. preprocess -> sign-free -> postprocess

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