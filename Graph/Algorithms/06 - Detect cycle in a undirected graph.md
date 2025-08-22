https://www.geeksforgeeks.org/problems/detect-cycle-in-an-undirected-graph/1

Given an **undirected graph** with **V** vertices and **E** edges, represented as a 2D vector **edges[][]**, where each entry `edges[i] = [u, v]` denotes an edge between vertices **u** and **v**, determine whether the graph contains a **cycle** or not.

**Examples:**

**Input:** `V = 4, E = 4, edges[][] = [[0, 1], [0, 2], [1, 2], [2, 3]]`
**Output:** true
**Explanation:** 

![|200](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/891735/Web/Other/blobid1_1743510240.jpg)   

`1 -> 2 -> 0 -> 1 is a cycle.`
### Intuition:
We will do DFS and keep exploring nodes in Depth first search way, if a node is already visited in this process then we can say there is cycle but that node should not be parent node since it is a undirected graph $u \to v$ == $v \to u$.

**Code:**


```java
class Solution {
    public boolean isCycle(int v, int[][] edges) {
        List<List<Integer>> adj = getAdjList(v, edges);
        boolean[] vis = new boolean[v];
        for (int i = 0; i < adj.size(); i++) {
            if (!vis[i] && hasCycle(vis, adj, i, -1)) {
                return true;
            }
        }
        
        return false;
    }
    
    private List<List<Integer>> getAdjList(int v, int[][] edges) {
        List<List<Integer>> adj = new ArrayList<>(v);
        for (int i = 0; i < v; i++) {
            adj.add(new ArrayList<>());
        }
        
        for (int[] edge : edges) {
            adj.get(edge[0]).add(edge[1]);
            adj.get(edge[1]).add(edge[0]);
        }
        return adj;
    }
    
    boolean hasCycle(boolean[] vis, List<List<Integer>> adj, int u, int par) {
        vis[u] = true;
        for (int v : adj.get(u)) {
            if (!vis[v]) {
                if (hasCycle(vis, adj, v, u)) {
                    return true;
                }
            } else {
                if (v != par) {
                    return true;
                }
            }
        }
        
        return false;
    }
}
```
