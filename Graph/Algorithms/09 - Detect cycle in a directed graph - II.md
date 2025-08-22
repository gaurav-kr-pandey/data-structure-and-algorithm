We can simply use - [[08 - Topological Sorting (Khan's BFS Based Algorithm)]].
Let's understand this -
In topo sort we process all the independent nodes and in this way process all the nodes eventually. So the idea is simple, if there is a cycle then, topo sort will not be able to process all the nodes because topo sort works only for `DAG`.

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