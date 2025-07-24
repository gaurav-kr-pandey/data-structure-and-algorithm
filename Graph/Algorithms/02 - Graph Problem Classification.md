
# 📘 Graph Problem Classification with Leetcode Examples

> ✅ Use this as a quick reference to match a problem type to an algorithm or technique.

## 📌 1. Traversal (DFS/BFS)
| Pattern    | Problem Name        | Leetcode Link | Approach |
|------------|---------------------|----------------|----------|
| Basic BFS  | Number of Islands   | [200](https://leetcode.com/problems/number-of-islands/) | BFS/DFS on Grid |
| Basic DFS  | Flood Fill          | [733](https://leetcode.com/problems/flood-fill/) | DFS |

## 📌 2. Connected Components
| Pattern              | Problem Name                   | Leetcode Link | Approach |
|----------------------|--------------------------------|----------------|----------|
| Count Components     | Number of Connected Components | [323](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/) | DFS/BFS |
| Grid-based Clusters  | Number of Provinces            | [547](https://leetcode.com/problems/number-of-provinces/) | DFS/Union-Find |

## 📌 3. Cycle Detection
| Pattern               | Problem Name         | Leetcode Link | Approach |
|-----------------------|----------------------|----------------|----------|
| Cycle in Undirected   | Graph Valid Tree     | [261](https://leetcode.com/problems/graph-valid-tree/) | DFS + parent |
| Cycle in Directed     | Course Schedule      | [207](https://leetcode.com/problems/course-schedule/) | DFS / Kahn's |

## 📌 4. Bipartite Graph
| Pattern      | Problem Name         | Leetcode Link | Approach |
|--------------|----------------------|----------------|----------|
| 2-color graph| Is Graph Bipartite?  | [785](https://leetcode.com/problems/is-graph-bipartite/) | BFS/DFS coloring |

## 📌 5. Shortest Path
| Pattern           | Problem Name            | Leetcode Link | Approach |
|-------------------|-------------------------|----------------|----------|
| Unweighted Graph  | Open the Lock           | [752](https://leetcode.com/problems/open-the-lock/) | BFS |
| Weighted Graph    | Network Delay Time      | [743](https://leetcode.com/problems/network-delay-time/) | Dijkstra |
| Negative Weights  | Cheapest Flights Within K Stops | [787](https://leetcode.com/problems/cheapest-flights-within-k-stops/) | Bellman-Ford |

## 📌 6. Topological Sort
| Pattern          | Problem Name       | Leetcode Link | Approach |
|------------------|--------------------|----------------|----------|
| Task Scheduling  | Course Schedule II | [210](https://leetcode.com/problems/course-schedule-ii/) | Kahn’s / DFS |
| Alien Dictionary | Alien Dictionary   | [269](https://leetcode.com/problems/alien-dictionary/) | Topo Sort |

## 📌 7. Minimum Spanning Tree (MST)
| Pattern    | Problem Name                   | Leetcode Link | Approach |
|------------|--------------------------------|----------------|----------|
| MST (Kruskal) | Min Cost to Connect All Points | [1584](https://leetcode.com/problems/min-cost-to-connect-all-points/) | Kruskal / Prim |

## 📌 8. Union-Find (DSU)
| Pattern             | Problem Name        | Leetcode Link | Approach |
|---------------------|---------------------|----------------|----------|
| Connectivity Query  | Number of Provinces | [547](https://leetcode.com/problems/number-of-provinces/) | DSU |
| Cycle Detection     | Redundant Connection| [684](https://leetcode.com/problems/redundant-connection/) | DSU |
| Grouping            | Accounts Merge      | [721](https://leetcode.com/problems/accounts-merge/) | DSU + Map |

## 📌 9. Grid as Graph
| Pattern           | Problem Name         | Leetcode Link | Approach |
|-------------------|----------------------|----------------|----------|
| Islands/Blob Count| Number of Islands    | [200](https://leetcode.com/problems/number-of-islands/) | BFS/DFS |
| Surrounded Region | Surrounded Regions   | [130](https://leetcode.com/problems/surrounded-regions/) | DFS + boundary |

## 📌 10. Advanced Graph
| Pattern              | Problem Name                        | Leetcode Link | Approach |
|----------------------|-------------------------------------|----------------|----------|
| Bridges in Graph     | Critical Connections                | [1192](https://leetcode.com/problems/critical-connections-in-a-network/) | Tarjan’s Algorithm |
| Articulation Points  | Min Days to Disconnect Island       | [1568](https://leetcode.com/problems/minimum-number-of-days-to-disconnect-island/) | Tarjan / DFS |
