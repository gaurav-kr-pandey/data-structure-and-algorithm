# 📘 Introduction to Graph in DSA
---
## 🔷 What is a Graph?
A **graph** is a data structure that consists of:
- A set of **vertices** (or nodes)
- A set of **edges** connecting pairs of vertices
### Graph Notation:

- G = (V, E), where:
    - V is a set of vertices
    - E is a set of edges (V × V)

---
## 🔷 Types of Graphs

|Type|Description|
|---|---|
|**Undirected**|Edges have no direction (A—B)|
|**Directed (Digraph)**|Edges have direction (A → B)|
|**Weighted**|Each edge has a weight/cost|
|**Unweighted**|No weights on edges|
|**Cyclic**|Contains at least one cycle|
|**Acyclic**|No cycles|
|**Connected**|There is a path between every pair of nodes|
|**Disconnected**|Some nodes are unreachable from others|

---
## 🔷 Graph Representations
### 1. **Adjacency Matrix**
- 2D array of size `V x V`
- `matrix[i][j] = 1` if there is an edge from i to j

```java
int V = 4; int[][] adjMatrix = new int[V][V];  // Add edge from 0 to 1 
adjMatrix[0][1] = 1; 
adjMatrix[1][0] = 1; // For undirected
```

**Pros:** Fast edge lookup  
**Cons:** Space complexity = O(V²)

---

### 2. **Adjacency List**
- Array/List of Lists
- Each index stores a list of adjacent vertices

```java
List<List<Integer>> adjList = new ArrayList<>();
int V = 4;

for (int i = 0; i < V; i++) {
    adjList.add(new ArrayList<>());
}

// Add edge
adjList.get(0).add(1);
adjList.get(1).add(0); // For undirected

```


**Pros:** Space-efficient (O(V + E))  
**Cons:** Slower edge lookup

---

## 🔷 Basic Graph Terminologies

- **Degree:** Number of edges incident to a vertex
    - In-degree / Out-degree for directed graphs
- **Path:** Sequence of vertices connected by edges
- **Cycle:** Path that starts and ends at the same vertex
- **Connected Component:** Maximal set of nodes reachable from each other

---

## 🔷 Traversal Techniques
### 1. **Breadth-First Search (BFS)**
- Level-wise traversal (Queue)
- Good for shortest path in unweighted graphs
```java
void bfs(int start, List<List<Integer>> graph, boolean[] visited) {
    Queue<Integer> queue = new LinkedList<>();
    queue.offer(start);
    visited[start] = true;

    while (!queue.isEmpty()) {
        int node = queue.poll();
        System.out.print(node + " ");

        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                queue.offer(neighbor);
            }
        }
    }
}

```

---

### 2. **Depth-First Search (DFS)**
- Recursive or Stack-based
- Good for cycle detection, connectivity

```java
void dfs(int node, List<List<Integer>> graph, boolean[] visited) {
    visited[node] = true;
    System.out.print(node + " ");

    for (int neighbor : graph.get(node)) {
        if (!visited[neighbor]) {
            dfs(neighbor, graph, visited);
        }
    }
}

```
---

## 🔷 Applications of Graphs
- Social networks
- Maps and navigation (shortest path)
- Web crawling
- Course scheduling (Topological Sort)
- Network broadcasting
- Cycle detection in dependencies


# 📘 Graphs in Data Structures - Basics

## 🔹 What is a Graph?

A **Graph** is a non-linear data structure consisting of:
- **Vertices (nodes)**: Entities or points
- **Edges**: Connections between nodes

A graph `G` is represented as:
G = (V, E)  
V = set of vertices  
E = set of edges (pairs of vertices)


---

## 🔹 Types of Graphs

### ➤ Directed vs Undirected
- **Directed Graph (Digraph)**: Edges have direction (A → B)
- **Undirected Graph**: Edges have no direction (A — B)

### ➤ Weighted vs Unweighted
- **Weighted Graph**: Each edge has a weight or cost
- **Unweighted Graph**: All edges are equal in cost (or no weights)

### ➤ Cyclic vs Acyclic
- **Cyclic Graph**: Contains at least one cycle
- **Acyclic Graph**: No cycles

### ➤ Connected vs Disconnected
- **Connected Graph** (undirected): There is a path between every pair of vertices
- **Disconnected Graph**: Not all vertices are reachable

---

## 🔹 Graph Terminologies

| Term                 | Description |
|----------------------|-------------|
| **Vertex (Node)**    | Fundamental unit of graph |
| **Edge**             | Connection between vertices |
| **Degree**           | Number of edges connected to a vertex |
| - Indegree           | Number of incoming edges (in directed graph) |
| - Outdegree          | Number of outgoing edges |
| **Path**             | Sequence of edges connecting vertices |
| **Cycle**            | A path where the first and last vertex are the same |
| **Connected Component** | A group of vertices connected directly or indirectly |

---

## 🔹 Applications of Graphs (Real World)

- **Social Networks**: Users as nodes, friendships as edges
- **Maps & Navigation**: Cities as nodes, roads as weighted edges
- **Web Crawling**: Web pages as nodes, hyperlinks as edges
- **Computer Networks**: Routers as nodes, network links as edges
- **Scheduling & Task Dependency**: DAGs for prerequisites
- **Recommendation Systems**: User-item graphs
- **Game Development**: Game state graphs, AI pathfinding

---

## ✅ Next Up:
- [[Graph Representation]]
- [[Graph Traversals - BFS and DFS]]
