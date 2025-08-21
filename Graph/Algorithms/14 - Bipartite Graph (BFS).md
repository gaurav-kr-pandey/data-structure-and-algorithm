
### 🔹 Definition
A **Bipartite Graph** is a graph whose vertices can be divided into **two disjoint sets** such that:
- Every edge connects a vertex from **set U** to **set V**
- No edge exists between vertices of the **same set**

👉 In other words, you can color the graph using **two colors** such that no two adjacent vertices have the same color.

---
#### 🔹 Examples
✅ Graph with even-length cycles or acyclic (tree) graphs → Bipartite  
❌ Graph with odd-length cycles → Not Bipartite

---
#### 🔹 Applications
- Matching problems (job assignment, stable marriage, etc.)
- Network flow
- Scheduling problems
- Social network analysis
---
#### 🔹 How to Check if a Graph is Bipartite?

We use **Graph Coloring**:
1. Assign a color (say 0) to a starting node.
2. Assign opposite color (1) to all its neighbors.
3. Continue using **BFS or DFS**.
4. If a conflict occurs (neighbor has the same color) → Not bipartite.

### Code:

```java
class Solution {
    public boolean isBipartite(int n, int[][] edges) {
        List<List<Integer>> graph = getAdj(edges, n);
        int[] color = new int[n];
        Arrays.fill(color, -1); // -1 means uncolored

        for (int i = 0; i < n; i++) {
            if (color[i] == -1) { // unvisited node -> new component
                if (!bfsCheck(i, graph, color)) {
                    return false;
                }
            }
        }
        return true;
    }

    private boolean bfsCheck(int start, List<List<Integer>> graph, int[] color) {
        Queue<Integer> q = new LinkedList<>();
        q.add(start);
        color[start] = 0;

        while (!q.isEmpty()) {
            int u = q.poll();
            for (int v : graph.get(u)) {
                if (color[v] == -1) {
                    color[v] = 1 - color[u]; // alternate color
                    q.add(v);
                } else if (color[v] == color[u]) {
                    return false;
                }
            }
        }
        return true;
    }

    private List<List<Integer>> getAdj(int[][] edges, int n) {
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < n; i++) adj.add(new ArrayList<>());
        for (int[] e : edges) {
            adj.get(e[0]).add(e[1]);
            adj.get(e[1]).add(e[0]);
        }
        return adj;
    }
}
```

### 🔹 Complexity

- **Time:** `O(V + E)` (visit all nodes and edges once)
- **Space:** `O(V + E)` (adjacency list + color array + queue/stack)

---
### 🔹 Key Notes
- Bipartite graphs **cannot** have **odd-length cycles**
- Graph having even-length cycles is Bipartite
- A **tree** is always bipartite (since it has no cycles)
- Checking bipartiteness = **2-coloring problem**