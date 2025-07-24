We can simply use - [[08 - Topological Sorting (Khan's BFS Based Algorithm)]]

### Code:


```java
public class CycleDetector {

    public static boolean hasCycle(int n, List<List<Integer>> adjList) {
        int[] indegree = new int[n];

        // Step 1: Compute indegree for all nodes
        for (int u = 0; u < n; u++) {
            for (int v : adjList.get(u)) {
                indegree[v]++;
            }
        }

        // Step 2: Enqueue all nodes with indegree 0
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0) {
                queue.add(i);
            }
        }

        // Step 3: Process nodes using Kahn's Algorithm
        int processedCount = 0;
        while (!queue.isEmpty()) {
            int node = queue.poll();
            processedCount++;

            for (int neighbor : adjList.get(node)) {
                indegree[neighbor]--;
                if (indegree[neighbor] == 0) {
                    queue.add(neighbor);
                }
            }
        }

        // Step 4: If all nodes were not processed, there's a cycle
        return processedCount != n;
    }
}
```