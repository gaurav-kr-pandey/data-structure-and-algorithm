Given a **undirected Graph** consisting of V vertices numbered from 0 to V-1 and E edges. The ith edge is represented by [ai,bi], denoting a edge between vertex ai and bi. We say two vertices u and v belong to a same component if there is a path from u to v or v to u. Find the number of **connected components** in the graph.
A connected component is a subgraph of a graph in which there exists a path between any two vertices, and no vertex of the subgraph shares an edge with a vertex outside of the subgraph.

**Examples:**
![](https://static.takeuforward.org/content/ProblemSetter-g_oC8sRD)

**Input:** V=4, edges=[[0,1],[1,2]]
**Output:** 2
**Explanation:** Vertices {0,1,2} forms the first component and vertex 3 forms the second component.

### Solution:
This problem is exactly same as - [[01 - Number of proviences]]
Both are **100% the same problem**, just framed differently.

```java
class Solution {
    public int connectedComponents(int[][] adj) {
        int n = adj.length;
        boolean[] visited = new boolean[n];
        int count = 0;

        for (int node = 0; node < n; node++) {
            if (!visited[node]) {
                dfs(adj, visited, node);
                count++; // One connected component finished
            }
        }

        return count;
    }

    private void dfs(int[][] adj, boolean[] visited, int node) {
        visited[node] = true;

        for (int neighbor = 0; neighbor < adj.length; neighbor++) {
            if (adj[node][neighbor] == 1 && !visited[neighbor]) {
                dfs(adj, visited, neighbor);
            }
        }
    }
}

```