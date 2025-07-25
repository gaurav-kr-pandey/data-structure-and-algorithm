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
public class PrimMST {

    // Represents an edge from current node u → v with weight
    static class Edge {
        int v;       // Destination vertex
        int weight;  // Edge weight

        Edge(int v, int weight) {
            this.v = v;
            this.weight = weight;
        }
    }

    // Pair used in PriorityQueue to store (node, weight)
    static class Pair {
        int node;    // Vertex
        int weight;  // Cost to reach this vertex

        Pair(int node, int weight) {
            this.node = node;
            this.weight = weight;
        }
    }

    public static int primMST(int n, List<List<Edge>> adjList) {
        boolean[] inMST = new boolean[n]; // Tracks nodes already included in MST
        PriorityQueue<Pair> minHeap = new PriorityQueue<>(Comparator.comparingInt(p -> p.weight));

        minHeap.add(new Pair(0, 0)); // Start from node 0 with cost 0
        int totalCost = 0;

        while (!minHeap.isEmpty()) {
            Pair current = minHeap.poll();
            int u = current.node;

            if (inMST[u]) continue; // Skip if already in MST

            inMST[u] = true;            // Include node u in MST
            totalCost += current.weight; // Add edge weight to total MST cost

            // Traverse all adjacent vertices (u → v)
            for (Edge edge : adjList.get(u)) {
                int v = edge.v;
                int wt = edge.weight;

                if (!inMST[v]) {
                    minHeap.add(new Pair(v, wt));
                }
            }
        }

        return totalCost;
    }

    /**
     * Adds an undirected edge u ↔ v with weight to the adjacency list.
     */
    private static void addEdge(List<List<Edge>> adjList, int u, int v, int wt) {
        adjList.get(u).add(new Edge(v, wt)); // u → v
        adjList.get(v).add(new Edge(u, wt)); // v → u (undirected)
    }

    // Example usage
    public static void main(String[] args) {
        int n = 5;
        List<List<Edge>> adjList = new ArrayList<>();
        for (int i = 0; i < n; i++) adjList.add(new ArrayList<>());

        // Constructing the undirected weighted graph
        addEdge(adjList, 0, 1, 2);  // 0 → 1 (2)
        addEdge(adjList, 0, 3, 6);  // 0 → 3 (6)
        addEdge(adjList, 1, 2, 3);  // 1 → 2 (3)
        addEdge(adjList, 1, 3, 8);  // 1 → 3 (8)
        addEdge(adjList, 1, 4, 5);  // 1 → 4 (5)
        addEdge(adjList, 2, 4, 7);  // 2 → 4 (7)

        int cost = primMST(n, adjList);
        System.out.println("Total cost of MST: " + cost);  // Output: 16
    }
}

```