## What is a Minimum Spanning Tree (MST)?

A **Minimum Spanning Tree** is a **subgraph** (specifically a tree) of a **connected, undirected, weighted graph** that:
1. **Connects all the vertices** together
2. **Uses exactly `V - 1` edges**, where `V` is the number of vertices
3. **Has no cycles**
4. **Minimises the total sum of edge weights**

In other words, **MST is the cheapest way to connect all nodes** without forming any cycle.

### 📌 Example:

Given a weighted graph:
```less
     1
A ------- B
|         |
4         2
|         |
C ------- D
     3

```

The **MST** would include:
- A → B (1)
- B → D (2)
- D → C (3)

**Total weight = 6**, and all 4 nodes are connected with 3 edges (a tree).

[[13 - Prim's Algorithm]]