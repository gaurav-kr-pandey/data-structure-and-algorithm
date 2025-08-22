https://www.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph/1

Given a Directed Graph with **V** vertices (Numbered from **0** to **V-1**) and **E** edges, check whether it contains any **cycle** or not.  
The graph is represented as a 2D vector `edges[][]`, where each entry `edges[i] = [u, v]` denotes an edge from vertices **u** to **v.**

**Examples:**

**Input:** `V = 4, edges[][] = [[0, 1], [0, 2], [1, 2], [2, 0], [2, 3]]`

![|200](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/700218/Web/Other/blobid0_1744197297.jpg)
**Output:** true
**Explanation**: The diagram clearly shows a cycle `0 → 2 → 0`
### Intuition:

**Incorrect:**
First approach that comes to our mind is using same approach as - [[06 - Detect cycle in a undirected graph]] but this solution won't work here, let's understand with example below -

![[Pasted image 20250822102254.png|350]]

In the above example if we start from node `0` then we will traverse node `1`, from node `1`
there is no other node to traverse so we we will start from node `2` and reach node `1` and see node `1` is already visited, hence we end up returning `true` but there is no cycle.

**Correct Approach:**
To solve above issue, what we can do is maintain visited nodes in current recursion stack and if we found any node already visited then we will be sure that given Graph has cycle. Let's understand this with the graph given below:

 ![[Pasted image 20250822105609.png|350]]

Here two DFS(0) and DFS(2) will be called because $0 \to 1$ and node `1` do not have any out-degree path, so basically we need to start from node `2` again. Let's observe each call carefully.

![[Pasted image 20250822110702.png|400]]

Hence if we can maintain a visited values for each recursion stack separately then we can solve this by detecting back edge in current recursion stack as described in above diagram.

**Code:**


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
