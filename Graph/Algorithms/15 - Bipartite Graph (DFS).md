## Idea
- Use **DFS** to color nodes recursively.
- Start from an uncolored node, assign a color (say `0`).
- For each neighbor:
    - If uncolored → assign the opposite color and recurse.
    - If already colored and has the same color as current → ❌ Not bipartite.

### Code:

```java
class Solution {
    public boolean isBipartite(int n, int[][] edges) {
        List<List<Integer>> graph = buildAdjList(edges, n);
        int[] color = new int[n];
        Arrays.fill(color, -1); // -1 means uncolored

        // Graph may be disconnected → check each component
        for (int i = 0; i < n; i++) {
            if (color[i] == -1) {
                if (!dfsCheck(i, 0, graph, color)) {
                    return false;
                }
            }
        }
        return true;
    }

    private boolean dfsCheck(int node, int c, List<List<Integer>> graph, int[] color) {
        color[node] = c;

        for (int neigh : graph.get(node)) {
            if (color[neigh] == -1) {
                // Assign opposite color and recurse
                if (!dfsCheck(neigh, 1 - c, graph, color)) {
                    return false;
                }
            } else if (color[neigh] == color[node]) {
                // Conflict → not bipartite
                return false;
            }
        }
        return true;
    }

    private List<List<Integer>> buildAdjList(int[][] edges, int n) {
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

## Complexity

- **Time:** `O(V + E)` (each node and edge is visited once).
- **Space:**
    - `O(V + E)` for adjacency list
    - `O(V)` for recursion stack (worst case in DFS).