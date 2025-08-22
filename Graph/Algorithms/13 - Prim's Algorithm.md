https://www.geeksforgeeks.org/problems/minimum-spanning-tree/1
## What is Prim’s Algorithm?

**Prim’s Algorithm** is a **greedy algorithm** used to find the MST.  
It **starts from any node**, and **grows the MST([[12 - Minimum Spanning Tree]]) one edge at a time**, always choosing the **minimum-weight edge** that connects a new node to the tree.

---

## High-Level Steps of Prim’s Algorithm

1. **Start** from any node (usually node `0`)
2. Use a **priority queue (min-heap)** to pick the edge with the **smallest weight**
3. **Expand** to the node that is not yet in MST
4. **Mark** the new node as part of MST
5. **Add all adjacent edges** from this node to the heap (only to unvisited nodes)
6. Repeat until all nodes are in MST

---

## Data Structures Used

|Data Structure|Purpose|
|---|---|
|`visited[]`|To track which nodes are already in MST|
|`PriorityQueue<Edge>`|To pick the next lightest edge|
|`Edge` class (or tuple): `(weight, from, to)`|Represents an edge|

---

## Time Complexity

- Using **priority queue (heap)** + adjacency list → `O(E log V)`  
    (E edges and heap operations take log V)

### Code:

```java
class Solution {
    class Edge {
        int from;
        int to;
        int weight;
        
        private Edge(int from, int to, int weight) {
            this.from = from;
            this.to = to;
            this.weight = weight;
        }
    }
    
    public int spanningTree(int v, int[][] edges) {
        
        int minCost = 0;
        PriorityQueue<Edge> pq = new PriorityQueue<>((e1, e2) -> e1.weight - e2.weight);
        boolean[] vis = new boolean[v];
        List<List<Edge>> list = getAdj(edges, v);
        
        if (list.isEmpty()) {
            return 0;
        }
        
        for (Edge edge : list.get(0)) {
            pq.add(edge);
        }
        
        vis[0] = true;
        
        while (!pq.isEmpty()) {
            Edge edge = pq.poll();
            int from = edge.from;
            int to = edge.to;
            int weight = edge.weight;
            
            if (vis[to]) continue;
            
            minCost += weight;
            vis[to] = true;
            
            for (Edge e : list.get(to)) {
                if (!vis[e.to]) {
                    pq.add(e);
                }
            }
        }
        
        return minCost;
        
    }
    
    private List<List<Edge>> getAdj(int[][] edges, int v) {
        List<List<Edge>> list = new ArrayList<>();
        for (int i = 0; i < v; i++) {
            list.add(new ArrayList<>());
        }
        
        for (int[]  edge : edges) {
            list.get(edge[0]).add(new Edge(edge[0], edge[1], edge[2]));
            list.get(edge[1]).add(new Edge(edge[1], edge[0], edge[2]));
        }
        
        return list;
    }
}
```