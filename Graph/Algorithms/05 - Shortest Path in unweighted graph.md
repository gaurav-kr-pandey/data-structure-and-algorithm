https://www.geeksforgeeks.org/problems/shortest-path-in-undirected-graph-having-unit-distance/1

You are given an adjacency list, **adj** of **Undirected Graph** having **unit weight** of the edges, find the shortest path from **src** to all the vertex and if it is **unreachable** to reach any vertex, then return **-1** for that vertex.

**Examples :**

**Input:** 
`adj[][]` = `[[1, 3], [0, 2], [1, 6], [0, 4], [3, 5], [4, 6], [2, 5, 7, 8], [6, 8], [7, 6]]`, 
`src = 0`
**Output:** `[0, 1, 2, 1, 2, 3, 3, 4, 4]`  
![|250](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/711976/Web/Other/blobid0_1745302423.jpg) 

### Intuition:

Since it is a unweighted graph, finding shortest path is exactly same as [[03 - Breadth First Search (BFS)]]. We just need to maintain a path integer with length `V = vertices`.

While traversing we can keep updating the `path[]` array. As given in the question that its a unweighted graph we can assume each edge to have `weight == 1`
weight to self is `0`.

### Code:

```java
class Solution {
    
    public int[] shortestPath(List<List<Integer>> adj, int src) {
        int n = adj.size();
        int[] path = new int[n];
        Arrays.fill(path, -1);
        boolean[] vis = new boolean[n];
        Queue<Integer> q = new LinkedList<>();
        q.add(src);
        vis[src] = true;
        path[src] = 0;
        
        while (!q.isEmpty()) {
            int u = q.poll();
            for (int v : adj.get(u)) {
                if (!vis[v]) {
                    vis[v] = true;
                    q.add(v);
                    path[v] = path[u] + 1;
                }
            }
        }
        
        return path;
    }
}
```