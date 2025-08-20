https://www.geeksforgeeks.org/problems/shortest-path-in-undirected-graph-having-unit-distance/1

You are given an adjacency list, **adj** of **Undirected Graph** having **unit weight** of the edges, find the shortest path from **src** to all the vertex and if it is **unreachable** to reach any vertex, then return **-1** for that vertex.

**Examples :**

**Input:** `adj[][]` = `[[1, 3], [0, 2], [1, 6], [0, 4], [3, 5], [4, 6], [2, 5, 7, 8], [6, 8], [7, 6]]`, `src = 0`
**Output:** `[0, 1, 2, 1, 2, 3, 3, 4, 4]`  
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/711976/Web/Other/blobid0_1745302423.jpg) 

**Input:** `adj[][]= [[3], [3], [], [0, 1]], src = 3`
**Output:** `[1, 1, -1, 0]`
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/711976/Web/Other/blobid0_1747111194.webp)

### Intuition:



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