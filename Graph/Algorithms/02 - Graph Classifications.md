
![[Pasted image 20250821195529.png]]


### 🧾 Graph Algorithms – Revision Notes
### 1. Graph Representation
- **Adjacency Matrix** → O(V²) space, easy edge existence check.  
- **Adjacency List** → O(V+E) space, efficient traversal (preferred in sparse graphs).  
---
### 2. Graph Traversal
#### BFS (Breadth First Search)
- **Time**: O(V+E)  
- **Space**: O(V) (queue + visited array)  
- **Use Cases**:
  - Shortest path in **unweighted graphs**  
  - Level-order processing  
  - Bipartite check  
#### DFS (Depth First Search)
- **Time**: O(V+E)  
- **Space**: O(V) (stack recursion + visited array)  
- **Use Cases**:
  - Cycle detection  
  - Topological Sort  
  - Connected components  
---
### 3. Cycle Detection
#### Undirected Graph
- **DFS + parent check** → O(V+E)  
- **Union-Find (Disjoint Set)** → O(E α(V))  
- **When**: Use Union-Find if graph is dynamic (many add-edge queries).  
#### Directed Graph
- **DFS + Recursion Stack** → O(V+E)  
- **Kahn’s Algorithm (Topo Sort)** → Detect cycle if not all nodes are processed.  
---
### 4. Topological Sort (DAG only)
- **DFS-based** → O(V+E)  
- **Kahn’s Algorithm (BFS + indegree)** → O(V+E)  
- **When**:  
  - DFS → better when recursion is fine.  
  - Kahn’s → useful to check **cycle existence**.  
---
### 5. Shortest Path Problems
#### Unweighted Graph
- **BFS** → O(V+E)  
#### Weighted Graph (Non-negative weights)
- **Dijkstra’s Algorithm**  
  - With min-heap → O((V+E) log V)  
  - With simple array → O(V²)  
- **When**: Efficient for sparse graphs with non-negative weights.  
#### Weighted Graph (Negative edges allowed, no negative cycle)
- **Bellman-Ford** → O(V·E)  
- **When**: Needed when negative edges exist (like currency arbitrage).  
#### DAG Shortest Path
- **Topo Order + Relax Edges** → O(V+E)  
- **When**: DAG is given → fastest possible.  
---
### 6. Minimum Spanning Tree (MST)
#### Prim’s Algorithm
- With min-heap → O((V+E) log V)  
- **When**: Better for dense graphs.  
#### Kruskal’s Algorithm
- Sorting edges → O(E log E)  
- Union-Find ops → O(E α(V))  
- **When**: Better for sparse graphs, easy to implement.  
---
### 7. Strongly Connected Components (SCC)
#### Kosaraju’s Algorithm
- **Steps**:
  1. DFS (finish time order)  
  2. Reverse graph  
  3. DFS in reverse order  
- **Time**: O(V+E)  
- **Space**: O(V+E)  
#### Tarjan’s Algorithm
- DFS + Low-link values  
- **Time**: O(V+E)  
- **Space**: O(V)  
- **When**: More memory efficient than Kosaraju.  
---
### 8. Articulation Points & Bridges
- **Tarjan’s Algorithm (DFS + Low-link values)**  
- **Time**: O(V+E)  
- **Space**: O(V)  
- **Use Cases**:
  - Network reliability (critical nodes/edges)  
---
### 9. Other Important Algorithms
- **Floyd-Warshall** → All pairs shortest path (with negatives, no cycle)  
  - Time: O(V³)  
  - Space: O(V²)  
  - **When**: Dense graphs, small V (~500).  

- **Union-Find (Disjoint Set Union – DSU)**  
  - Used in Kruskal, dynamic connectivity.  
  - Time: ~O(α(V)) per operation.  
---
#### 🔑 Summary Table (When to Use What)

| Problem                       | Best Algo         | Time           | Space  | Notes                       |
| ----------------------------- | ----------------- | -------------- | ------ | --------------------------- |
| Traversal                     | BFS/DFS           | O(V+E)         | O(V)   | DFS = deep, BFS = level     |
| Cycle (Undirected)            | DFS / Union-Find  | O(V+E)         | O(V)   | Union-Find for dynamic      |
| Cycle (Directed)              | DFS / Kahn’s      | O(V+E)         | O(V)   | Kahn detects cycle          |
| Shortest Path (Unweighted)    | BFS               | O(V+E)         | O(V)   |                             |
| Shortest Path (Weighted, +ve) | Dijkstra          | O((V+E) log V) | O(V+E) | Min-heap                    |
| Shortest Path (Neg. edges)    | Bellman-Ford      | O(V·E)         | O(V)   | Detect neg cycle            |
| Shortest Path (DAG)           | Topo + Relax      | O(V+E)         | O(V)   | Best for DAG                |
| All Pairs Shortest Path       | Floyd-Warshall    | O(V³)          | O(V²)  | Small V                     |
| MST (Dense)                   | Prim’s            | O((V+E) log V) | O(V+E) |                             |
| MST (Sparse)                  | Kruskal’s         | O(E log E)     | O(V+E) | Easier with DSU             |
| SCC                           | Kosaraju / Tarjan | O(V+E)         | O(V+E) | Tarjan more space efficient |
| Articulation/Bridges          | Tarjan’s          | O(V+E)         | O(V)   | Critical nodes/edges        |

---
### 📚 Suggested Order of Learning
1. **BFS/DFS** → foundation.  
2. **Cycle detection** → both directed & undirected.  
3. **Topological Sort (DFS/Kahn)**.  
4. **Shortest Path** (BFS → Dijkstra → Bellman-Ford → DAG → Floyd).  
5. **MST** (Prim/Kruskal).  
6. **SCC** (Kosaraju/Tarjan).  
7. **Articulation Points & Bridges**.  
---

### 📘 Graph Problem Classification with Leetcode Examples

> ✅ Use this as a quick reference to match a problem type to an algorithm or technique.

#### 📌 1. Traversal (DFS/BFS)
| Pattern   | Problem Name      | Leetcode Link                                           | Approach        |
| --------- | ----------------- | ------------------------------------------------------- | --------------- |
| Basic BFS | Number of Islands | [200](https://leetcode.com/problems/number-of-islands/) | BFS/DFS on Grid |
| Basic DFS | Flood Fill        | [733](https://leetcode.com/problems/flood-fill/)        | DFS             |

#### 📌 2. Connected Components
| Pattern             | Problem Name                   | Leetcode Link                                                                               | Approach       |
| ------------------- | ------------------------------ | ------------------------------------------------------------------------------------------- | -------------- |
| Count Components    | Number of Connected Components | [323](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/) | DFS/BFS        |
| Grid-based Clusters | Number of Provinces            | [547](https://leetcode.com/problems/number-of-provinces/)                                   | DFS/Union-Find |

#### 📌 3. Cycle Detection
| Pattern             | Problem Name     | Leetcode Link                                          | Approach     |
| ------------------- | ---------------- | ------------------------------------------------------ | ------------ |
| Cycle in Undirected | Graph Valid Tree | [261](https://leetcode.com/problems/graph-valid-tree/) | DFS + parent |
| Cycle in Directed   | Course Schedule  | [207](https://leetcode.com/problems/course-schedule/)  | DFS / Kahn's |

#### 📌 4. Bipartite Graph
| Pattern       | Problem Name        | Leetcode Link                                            | Approach         |
| ------------- | ------------------- | -------------------------------------------------------- | ---------------- |
| 2-color graph | Is Graph Bipartite? | [785](https://leetcode.com/problems/is-graph-bipartite/) | BFS/DFS coloring |

#### 📌 5. Shortest Path
| Pattern          | Problem Name                    | Leetcode Link                                                         | Approach     |
| ---------------- | ------------------------------- | --------------------------------------------------------------------- | ------------ |
| Unweighted Graph | Open the Lock                   | [752](https://leetcode.com/problems/open-the-lock/)                   | BFS          |
| Weighted Graph   | Network Delay Time              | [743](https://leetcode.com/problems/network-delay-time/)              | Dijkstra     |
| Negative Weights | Cheapest Flights Within K Stops | [787](https://leetcode.com/problems/cheapest-flights-within-k-stops/) | Bellman-Ford |

#### 📌 6. Topological Sort
| Pattern          | Problem Name       | Leetcode Link                                            | Approach     |
| ---------------- | ------------------ | -------------------------------------------------------- | ------------ |
| Task Scheduling  | Course Schedule II | [210](https://leetcode.com/problems/course-schedule-ii/) | Kahn’s / DFS |
| Alien Dictionary | Alien Dictionary   | [269](https://leetcode.com/problems/alien-dictionary/)   | Topo Sort    |

#### 📌 7. Minimum Spanning Tree (MST)
| Pattern       | Problem Name                   | Leetcode Link                                                         | Approach       |
| ------------- | ------------------------------ | --------------------------------------------------------------------- | -------------- |
| MST (Kruskal) | Min Cost to Connect All Points | [1584](https://leetcode.com/problems/min-cost-to-connect-all-points/) | Kruskal / Prim |

#### 📌 8. Union-Find (DSU)
| Pattern            | Problem Name         | Leetcode Link                                              | Approach  |
| ------------------ | -------------------- | ---------------------------------------------------------- | --------- |
| Connectivity Query | Number of Provinces  | [547](https://leetcode.com/problems/number-of-provinces/)  | DSU       |
| Cycle Detection    | Redundant Connection | [684](https://leetcode.com/problems/redundant-connection/) | DSU       |
| Grouping           | Accounts Merge       | [721](https://leetcode.com/problems/accounts-merge/)       | DSU + Map |

#### 📌 9. Grid as Graph
| Pattern            | Problem Name       | Leetcode Link                                            | Approach       |
| ------------------ | ------------------ | -------------------------------------------------------- | -------------- |
| Islands/Blob Count | Number of Islands  | [200](https://leetcode.com/problems/number-of-islands/)  | BFS/DFS        |
| Surrounded Region  | Surrounded Regions | [130](https://leetcode.com/problems/surrounded-regions/) | DFS + boundary |

#### 📌 10. Advanced Graph
| Pattern             | Problem Name                  | Leetcode Link                                                                      | Approach           |
| ------------------- | ----------------------------- | ---------------------------------------------------------------------------------- | ------------------ |
| Bridges in Graph    | Critical Connections          | [1192](https://leetcode.com/problems/critical-connections-in-a-network/)           | Tarjan’s Algorithm |
| Articulation Points | Min Days to Disconnect Island | [1568](https://leetcode.com/problems/minimum-number-of-days-to-disconnect-island/) | Tarjan / DFS       |
