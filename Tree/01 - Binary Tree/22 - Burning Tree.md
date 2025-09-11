https://www.geeksforgeeks.org/problems/burning-tree/1

Given a binary tree and a **target** node, determine the minimum time required to burn the entire tree if the **target** node is set on fire. In one second, the fire spreads from a node to its left child, right child, and parent.  
**Note:** The tree contains unique values.

**Examples :** 

**Input:** root[] = `[1, 2, 3, 4, 5, 6, 7]`, target = 2  

![|250](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/702131/Web/Other/blobid0_1747048733.webp)

**Output:** 3
**Explanation:** Initially 2 is set to fire at 0 sec   
At 1 sec: Nodes 4, 5, 1 catches fire.  
At 2 sec: Node 3 catches fire.  
At 3 sec: Nodes 6, 7 catches fire.  
It takes 3s to burn the complete tree.

## Intuition:

Ref: [[04 - Rotten Oranges]]

## Code:

```java
class Solution {
    public int minTime(Node root, int target) {
        Map<Integer, List<Node>> adj = new HashMap<>();
        build(root, null, adj);
        
        Queue<Integer> q = new LinkedList<>();
        Set<Integer> seen = new HashSet<>();
        q.add(target);
        seen.add(target);
        int time = 0;
        
        while (!q.isEmpty()) {
            int size = q.size();
            while (size-- > 0) {
                int curr = q.poll();
                List<Node> list = adj.get(curr);
                
                for (Node v : list) {
                    if (!seen.contains(v.data)) {
                        q.add(v.data);
                        seen.add(v.data);
                    }
                }
            }   
            time++;
        }
        
        return time - 1;
    }
    
    private void build(Node curr, Node par, Map<Integer, List<Node>> adj) {
        if (curr == null) return;
        
        List<Node> list = adj.getOrDefault(curr, new ArrayList<>());
        adj.putIfAbsent(curr.data, list);
        if (par != null) {
            list.add(par);
            adj.get(par.data).add(curr);
        }
        
        build(curr.left, curr, adj);
        build(curr.right, curr, adj);
    }
}
```