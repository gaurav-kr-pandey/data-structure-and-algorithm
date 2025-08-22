https://www.geeksforgeeks.org/problems/topological-sort/1
## What is Topological Sort?

Topological Sorting of a **Directed Acyclic Graph (DAG)** is a linear ordering of its vertices such that for every directed edge `u → v`, **`u` appears before `v`** in the ordering.

> ⚠️ Only valid for **DAGs** (Directed Acyclic Graphs)

---

## Kahn’s Algorithm (BFS-Based Topo Sort)

### Idea:
- Nodes with **0 indegree** have no dependencies.
- Start from nodes with 0 indegree and **remove them from the graph**.
- As we remove them, **reduce indegree** of their neighbors.
- If any neighbor’s indegree becomes 0, it becomes eligible next.

---

## 📋 Steps:

1. **Calculate indegree** of every node.
2. **Add all 0-indegree nodes** to a queue.
3. While queue is not empty:
   - Pop a node from the queue and add it to the result.
   - For each neighbor:
     - Decrease its indegree by 1.
     - If indegree becomes 0, add to queue.
4. If result contains all nodes → valid topological sort.
   - Else → graph contains a **cycle** (Not a DAG).

---

#### Code:

```java
class Solution {

    public static ArrayList<Integer> topoSort(int n, int[][] edges) {
        List<List<Integer>> adj = getAdjList(edges, n);

        int[] indegree = new int[n];
        for (int i = 0; i < n; i++) {
            for (int v : adj.get(i)) {
                indegree[v]++;
            }
        }

        boolean[] vis = new boolean[n];
        Queue<Integer> q = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0) {
                q.add(i);
                vis[i] = true;
            }
        }

        ArrayList<Integer> topo = new ArrayList<>();
        while (!q.isEmpty()) {
            int u = q.poll();
            topo.add(u);
            for (int v : adj.get(u)) {
                if (!vis[v]) {
                    indegree[v]--;
                    if (indegree[v] == 0) {
                        q.add(v);
                        vis[v] = true;
                    }
                }
            }
        }

        if (topo.size() != n) {
            // Graph has a cycle
            return new ArrayList<>(); 
            // or throw new IllegalArgumentException("Cycle detected")
        }

        return topo;
    }

    private static List<List<Integer>> getAdjList(int[][] edges, int v) {
        List<List<Integer>> adj = new ArrayList<>();
        for (int i = 0; i < v; i++) {
            adj.add(new ArrayList<>());
        }

        for (int[] edge : edges) {
            adj.get(edge[0]).add(edge[1]);
        }

        return adj;
    }
}

```
