
### **Intuition Behind the DFS Approach**

1. **DFS explores deep first**, so we can use that to visit a node and **recursively finish all its dependencies** before marking it as complete.
2. Once all children of a node are processed, we know this node has no unvisited dependencies left → **we can now safely place it in the ordering**.
3. To maintain the correct order:
    - We use a **stack** (or reverse a list).
    - After visiting all neighbours of a node, we **push it to the stack** — this guarantees that nodes with no outgoing edges are added first (like leaf nodes), and dependencies are added later.

### Code:


```java
public class TopoSortDFS {

    public static List<Integer> topologicalSort(int n, List<List<Integer>> adjList) {
        boolean[] visited = new boolean[n];
        Stack<Integer> stack = new Stack<>();
        
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                dfs(i, adjList, visited, stack);
            }
        }

        List<Integer> topoOrder = new ArrayList<>();
        while (!stack.isEmpty()) {
            topoOrder.add(stack.pop());
        }

        return topoOrder;
    }

    private static void dfs(int node, List<List<Integer>> adjList, boolean[] visited, Deque<Integer> stack) {
        visited[node] = true;

        for (int neighbor : adjList.get(node)) {
            if (!visited[neighbor]) {
                dfs(neighbor, adjList, visited, stack);
            }
        }

        stack.push(node);  // Post-order: add after visiting all neighbors
    }
}

```