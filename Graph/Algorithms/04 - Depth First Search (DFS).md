https://www.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1

**Depth First Search (DFS)** is a **graph traversal algorithm** that explores as far as possible along each branch before backtracking.
- Uses **Recursion (Stack)** or explicit **Stack** data structure.
- Traverses graph in a **depth-wise manner**.

### Characteristics

- Traverses graph **deep before wide**.
- Works on both **directed & undirected graphs**.
- Time Complexity:
    - **O(V + E)** (V = vertices, E = edges).
- Space Complexity:
    - **O(V)** for visited + recursion/stack.
- Does **not guarantee shortest path** in unweighted graphs.

### Code:

```java
class Solution {
    
    public List<Integer> dfs(List<List<Integer>> adj) {
        List<Integer> list = new ArrayList<>();
        boolean[] vis = new boolean[adj.size()];
        dfs(adj, list, vis, 0);
        return list;
    }
    
    void dfs(List<List<Integer>> adj, List<Integer> list, boolean[] vis, int u) {
        vis[u] = true;
        list.add(u);
        for (int v : adj.get(u)) {
            if (!vis[v]) {
                dfs(adj, list, vis, v);
            }
        }
    }
} 
```


### Applications of DFS

1. **Detecting Cycles** in directed/undirected graphs.
2. **Topological Sorting** (DAGs).
3. **Finding Connected Components**.
4. **Solving Mazes / Backtracking problems**.
5. **Detecting Bridges and Articulation Points** in networks.
6. **Checking for Strongly Connected Components (SCC)** (Tarjan/Kosaraju).

---
### Variations
- **Recursive DFS**: Uses system call stack.
- **Iterative DFS**: Uses explicit stack.
- **Multi-source DFS**: Start DFS from multiple unvisited nodes for disconnected graphs.