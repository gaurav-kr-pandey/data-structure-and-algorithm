https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/description/

Given the `root` of a binary tree, the value of a target node `target`, and an integer `k`, return _an array of the values of all nodes that have a distance_ `k` _from the target node._
You can return the answer in **any order**.

**Example 1:**
![|250](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/06/28/sketch0.png)

**Input:** root = `[3,5,1,6,2,0,8,null,null,7,4]`, target = `5`, k = `2`
**Output:** `[7,4,1]`
**Explanation:** The nodes that are a distance 2 from the target node (with value 5) have values 7, `4`, and `1`.

## Intuition:
If you look closely, we need to traverse in all direction `target` node is connected to, even path through `parent` node as well. In normal traversal of Binary Tree, we traverse left and right child and do not have access to parent node. 
With above intuition this looks a problem of graph to print all the nodes `k` distance away from source node. We can do BFS traversal to achieve this.
But, how to do BFS we need adjacency list representation of given Binary Tree. Here is the algo:

```text
1. Build bi-directional adjacency list from root node
2. Start BFS from target node
3. Keep decrementing k after all the u -> v is explored for current level
4. If k == 0, add it to the answer list
```

## Code:

```java
class Solution {
    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        Map<TreeNode, List<TreeNode>> list = buildGraph(root);
        List<Integer> dis = new ArrayList<>();
        Queue<TreeNode> q = new LinkedList<>();
        Set<Integer> seen = new HashSet<>();
        q.add(target);
        seen.add(target.val);
        
        while (!q.isEmpty()) {
            int size = q.size();
            while (size-- > 0) {
                TreeNode curr = q.poll();
                if (k == 0) {
                    dis.add(curr.val);
                }

                for (TreeNode v : list.get(curr)) {
                    if (!seen.contains(v.val)) {
                        q.add(v);
                        seen.add(v.val);
                    }
                }
            }
            k--;
        }

        return dis;
    }

    private Map<TreeNode, List<TreeNode>> buildGraph(TreeNode root) {
        Map<TreeNode, List<TreeNode>> adj = new HashMap<>();
        build(root, null, adj);
        return adj;
    }

    private void build(TreeNode curr, TreeNode par, Map<TreeNode, List<TreeNode>> adj) {
        if (curr == null) {
            return;
        }
        List<TreeNode> list = adj.getOrDefault(curr, new ArrayList<>());
        adj.putIfAbsent(curr, list);
        if (par != null) {
            list.add(par);
            adj.get(par).add(curr);
        }

        build(curr.left, curr, adj);
        build(curr.right, curr, adj);
    }
}
```