```java
class Solution {
    
    public ArrayList<Integer> bfs(ArrayList<ArrayList<Integer>> adj) {
        
        ArrayList<Integer> list = new ArrayList<>();
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