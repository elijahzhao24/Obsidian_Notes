![](../../../pasted_images/Pasted%20image%2020260717181830.png)

## a) (10 pts.) Use induction to show that an A-ranking always exists.

**Base case:** n = 1

If there is only one deck, the ordering is automatically an A-ranking.

There are no consecutive pairs that need to be checked.  

**Inductive hypothesis:**

Assume that every tournament containing n decks have an A-ranking

**Inductive Step:**

Consider any tournament containing $n+1$ decks.

Choose one deck $(x)$ and remove it. The remaining n decks still have an A-ranking from inductive hypothesis. 

This also means that $(d_i,d_{i+1})\in E$, for every $(1\leq i<n)$ in the ranking.

We now insert $x$ back into this ranking.

Starting from $d_1$, find the first deck $d_i$ that $x$ defeats, meaning: $(x, d_i) \in E$
###### in the case where $(x, d_1)$ is the first edge: 
- place x at the beginning $[ x,d_1,d_2,\ldots,d_{n} ]$
- It is an A-ranking because $x$ defeats $d_1$ and all the original consecutive edges still remain valid.
###### in the case where i > 1: 
- because $d_i$ is the first deck that $x$ defeats, $x$ does not defeat $d_{i-1}$
	- since the deck is tournament, exactly one of the edges $(x,d_{i-1})$  or $(d_{i-1},x)$ exist
	-  we know it's  $(d_{i-1},x)$ , because $d_i$ is the first deck that $x$ defeats
- This means we can slide $x$ between $d_{i-1}$ and $d_{i}$
	- $d_1,\ldots,d_{i-1},x,d_i,\ldots,d_{n}.$
	- $(d_{i−1}​,x)∈E$ and $(x,d_i​)∈E.$
###### in the case where x defeats no decks 
- Then every deck defeats $x$, in particular, $(d_{n},x)$
- Therefore, place $x$ at the end:
	- $d_1,d_2,\ldots,d_{n},x.$

Because we can insert $x$ into the A-ranking of the other $n$ decks to obtain an A-ranking of all $n+1$ decks, by induction, an A-ranking exists for every tournament.


## b) (5 pts.) Provide pseudocode for a correct and efficient algorithm to find a ranking, given a tournament. You don’t need to prove correctness here, but briefly justify a good asymptotic bound on the worst-case runtime of your algorithm

Some version of post order dfs.

```
keep track of a visited set 
keep track of a stack

loop through all decks:
	if that deck is not yet in the visited set:
		Run a post order dfs where:
			Add that deck to that visited set.
			
			First call dfs on all outbound decks that have not been visited yet.
			Add current deck to stack.

Create a list 

while the stack is not empty:
	Pop from the stack and add that to the list (This reverses the stack)

This list with the reversed order of the stack is a valid A-ranking
```

Worst case time complexity is **O(V+E)**, because we are visiting all decks once during the topological sort, and once every deck, we also visit all the outbound edges for that deck.

Reversing the stack is only a O(V) operation, not the dominating factor.

## 3) (5 points) Boris does not think that A-rankings are good rankings. According to him, a deck with the smallest outdegree (less wins) could be first in some A-rankings. Help him find an example of this.

![](../../../pasted_images/Pasted%20image%2020260717195549.png)

The following picture shows the following Decks, Matches, and out degrees:

```
Decks (vertices) = {A,B,C,D,E,F}

Matches (edges) = {
	(A,B),
	(B,C), (B,D),
	(C,A), (C,D), (C,E),
	(D,A), (D,E), (D,F),
	(E,A), (E,B), (E,F),
	(F,A), (F,B), (F,C)
}

Outdegrees = {
	A: 1,
	B: 2,
	C: 3,
	D: 3,
	E: 3,
	F: 3
}
```

Despite A  only having one win (one out degree), a valid A-ranking can still be made with A at the start

```
[A, B, C, D, E, F]
```

#### d) (10 pts.) Boris proposes another definition of “good ranking”: a B-ranking is any permutation of decks d1, . . . , dn such that δ +(di) ≥ δ +(di+1) ∀i ∈ {1, . . . , n − 1}. Here δ +(v) denotes the out-degree4 of v. Show that if a deck d has the first place in a B-ranking, then it has the following nice property: for every other deck v, either (d, v) ∈ E or there is another deck u such that (d, u) ∈ E and (u, v) ∈ E.

###### Trivial case:
if D has a outbound edge to every deck (which also means it's outbound edges must be the max of all decks), the property exists.

###### Hard case:
Let d be the deck in first place in a B-ranking.

Because a B-ranking sorts decks from highest outdegree to lowest outdegree, d has maximum outdegree. Therefore, d has at least as many wins as every other deck.

Now consider any other deck v.
- If d defeats v, then the property is already satisfied.
- Otherwise, v defeats d, since exactly one directed edge exists between every pair of decks in a tournament.

**Suppose, for contradiction, that there is no deck u such that d defeats u and u defeats v.**

Consider every deck u that d defeats. Since we assumed that u does not defeat v, and this is a tournament, v must defeat u.
- Therefore, v defeats d and every deck that d defeats.

If d has k wins, then v has at least k + 1 wins: one win against d, plus one win against each of the k decks defeated by d.
- This means that v has more wins than d.
- However, d is first in the B-ranking, so d must have at least as many wins as v. This is a contradiction.

Therefore, our assumption was false. There must be some deck u such that d defeats u and u defeats v.

Thus, for every other deck v, either d defeats v directly, or d defeats another deck u that defeats v.

## e) (5 pts.) Chen is concerned that in a B-ranking, the second best may beat the best, which may look odd. She proposes yet another definition of “good ranking”: a C-ranking is any permutation which is both an A-ranking and a B-ranking. Either show a tournament graph where no C-ranking exists or provide an algorithm that outputs a C-ranking for any tournament graph

Using the same example from part c).

```
the outdegrees are:

Outdegrees = {
	A: 1,
	B: 2,
	C: 3,
	D: 3,
	E: 3,
	F: 3
}
```

Which means according to B-ranking, it must have this kind of structure: 
```
[C, D, E, F in some order], B, A
```

For this ranking to also be an A-ranking, we would need the edge: $(B, A) \in E$

However this edge does not exist in our edge list:
```
Matches (edges) = {
	(A,B),
	(B,C), (B,D),
	(C,A), (C,D), (C,E),
	(D,A), (D,E), (D,F),
	(E,A), (E,B), (E,F),
	(F,A), (F,B), (F,C)
}
```

Therefore, no B-ranking of this tournament is also an A-ranking. Therefore, this tournament has no C-ranking.