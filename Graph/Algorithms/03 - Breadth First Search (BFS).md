**Breadth First Search (BFS)** is a **graph traversal algorithm** that explores vertices in the order of their distance from the source node (level by level).
- Uses **Queue (FIFO)** data structure.
- Ensures shortest path in an **unweighted graph**.

### Characteristics
- Traverses graph **level by level**.
- Works on both **directed & undirected graphs**.
- Time Complexity:
    - **O(V + E)** (V = vertices, E = edges).
- Space Complexity:
    - **O(V)** for visited + queue.
- Guarantees **shortest path** (in terms of edge count) in **unweighted graphs**.


**Code:**
```java
class Solution {
    
    public List<Integer> bfs(List<List<Integer>> adj) {
        
        List<Integer> list = new ArrayList<>();
        boolean[] vis = new boolean[adj.size()];
        Queue<Integer> q = new LinkedList<>();
        q.add(0);
        vis[0] = true;
        
        while (!q.isEmpty()) {
            int u = q.poll();
            list.add(u);
            
            for (int v : adj.get(u)) {
                if (!vis[v]) {
                    vis[v] = true;
                    q.add(v);
                }
            }
        }
        
        return list;
    }
}
```

### Applications of BFS
1. **Shortest Path in Unweighted Graph** (e.g., finding minimum edges).
2. **Connected Components** detection.
3. **Cycle detection** in undirected graphs.
4. **Level Order Traversal** of Trees (BFS is equivalent).
5. **Web Crawlers / Social Network Search** (friends-of-friends).
6. **Bipartite Graph Check**.

### Variations
- **Multi-source BFS**: Start from multiple nodes simultaneously.
- **0-1 BFS**: For weighted graphs with edges 0 or 1 → use **Deque**.
- **Bidirectional BFS**: For shortest path search between 2 nodes.