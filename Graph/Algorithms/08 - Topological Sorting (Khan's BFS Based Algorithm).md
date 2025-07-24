
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

## ✅ Code (Java)


```java
public List<Integer> topoSort(int V, List<List<Integer>> adj) {
    int[] indegree = new int[V];
    for (int u = 0; u < V; u++) {
        for (int v : adj.get(u)) {
            indegree[v]++;
        }
    }

    Queue<Integer> q = new LinkedList<>();
    for (int i = 0; i < V; i++) {
        if (indegree[i] == 0) q.add(i);
    }

    List<Integer> topo = new ArrayList<>();
    while (!q.isEmpty()) {
        int u = q.poll();
        topo.add(u);
        for (int v : adj.get(u)) {
            indegree[v]--;
            if (indegree[v] == 0) q.add(v);
        }
    }

    if (topo.size() != V) {
        throw new RuntimeException("Graph has a cycle");
    }

    return topo;
}
