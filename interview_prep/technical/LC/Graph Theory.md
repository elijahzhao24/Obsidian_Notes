


# Hierholzer's Algorithm (finding Eulerian Path)

#### Data structures:

- adjacency list
- final path Array (result)
#### Complexity:

Time: `O(V+E)` or technically `O(E)` because you are just processing edges
Space: `O(V + E)` (can also be simplified to `O(E)`)
#### Eulerian Path definition
> An **Eulerian Path** is a path through a graph that uses **every edge exactly once**. **edges matter, not vertices**. You can visit the same vertex multiple times, but you cannot reuse an edge.

 A Eulerian Circuit is a Eulerian path that starts and ends on the same node.

A Eulerian Path exists if exactly 2 or 0 "odd" vertices exists:
```
one node with out-degree = in-degree + 1   // start
one node with in-degree = out-degree + 1   // end
all others have in-degree == out-degree

0 "odd" vertices means a circuit exists.
```

#### Algorithm

It is a post order DFS algorithm:
- Keep traversing unused edges.  
- When you cannot traverse anymore (no more out-degrees), this node belongs at the END of the answer.  
- Append it.  
- Reverse at the end.

Intution: Hierholzer’s algorithm is like DFS/backtracking, but instead of “trying choices and undoing,” you consume each edge exactly once, and when a node has no outgoing edges left, you add it to the final answer.

pseudocode code:
```python
# make sure Eulerian Path
# find start node
# run dfs(start)
# reverse your path/res

def dfs(node):
    while node has outgoing edges:
        next = remove one outgoing edge from node
        dfs(next)

    path.append(node)
```