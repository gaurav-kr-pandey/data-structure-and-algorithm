```java
class Solution {
    
    public ArrayList<Integer> dfs(ArrayList<ArrayList<Integer>> adj) {
        ArrayList<Integer> list = new ArrayList<>();
        boolean[] vis = new boolean[adj.size()];
        dfs(adj, list, vis, 0);
        return list;
    }
    
    void dfs(ArrayList<ArrayList<Integer>> adj, ArrayList<Integer> list, boolean[] vis, int u) {
        vis[u] = true;
        list.add(u);
        for (int v : adj.get(u)) {
            if (!vis[v]) {
                dfs(adj, list, vis, v);
            }
        }
    }
} 
```