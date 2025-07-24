https://www.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1

Given a Directed Graph with **V** vertices (Numbered from **0** to **V-1**) and **E** edges, check whether it contains any **cycle** or not.  
The graph is represented as a 2D vector **edges[][]**, where each entry **edges[i] = [u, v]** denotes an edge from vertices **u** to **v.**

**Examples:**

**Input:** V = 4, edges[][] = [[0, 1], [0, 2], [1, 2], [2, 0], [2, 3]]
![](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700218/Web/Other/blobid0_1744197297.jpg)
**Output:** true
**Explanation**: The diagram clearly shows a cycle 0 → 2 → 0

### Solution:

```java
class Solution {
    public boolean isCyclic(int numVertices, int[][] edges) {
        List<List<Integer>> adjList = buildAdjList(numVertices, edges);
        boolean[] visited = new boolean[numVertices];
        boolean[] recursionStack = new boolean[numVertices];

        for (int node = 0; node < numVertices; node++) {
            if (!visited[node] && hasCycleDFS(node, visited, recursionStack, adjList)) {
                return true;
            }
        }

        return false;
    }

    private List<List<Integer>> buildAdjList(int numVertices, int[][] edges) {
        List<List<Integer>> adjList = new ArrayList<>();
        for (int i = 0; i < numVertices; i++) {
            adjList.add(new ArrayList<>());
        }

        for (int[] edge : edges) {
            adjList.get(edge[0]).add(edge[1]); // Directed edge
        }

        return adjList;
    }

    private boolean hasCycleDFS(int node, boolean[] visited, boolean[] recursionStack, List<List<Integer>> adjList) {
        visited[node] = true;
        recursionStack[node] = true;

        for (int neighbor : adjList.get(node)) {
            if (!visited[neighbor] && hasCycleDFS(neighbor, visited, recursionStack, adjList)) {
                return true;
            }
            if (recursionStack[neighbor]) {
                return true;
            }
        }

        recursionStack[node] = false; // backtrack
        return false;
    }
}
```
