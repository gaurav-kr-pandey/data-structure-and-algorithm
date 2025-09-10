https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/description/

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

**Input:** root = `[3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1`
**Output:** 3
**Explanation:** The LCA of nodes 5 and 1 is 3.

### Intuition
- If the current root is `null` → return `null`.  
- If the root is equal to `p` or `q` → root itself is part of the answer.  
- Otherwise:
  - Recurse left and right.
  - If both return non-null → current root is the **lowest common ancestor**.
  - If only one side returns non-null → propagate that result upward.
### Approach
- Use **DFS recursion**.
- At each step, decide whether:
  - Current node is one of the targets.
  - Both targets are in different subtrees.
  - Both are in the same subtree.
### Code

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) {
            return null;
        }
        if (root == p || root == q) {
            return root;
        }

        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);

        if (left != null && right != null) {
            return root;
        }

        return (left != null) ? left : right;
    }
}
```

### Complexity
- **Time:** O(n), where n = number of nodes (worst case: visit all nodes).
- **Space:** O(h), where h = height of the tree (recursion stack). Worst case O(n), balanced case O(log n).

#### What if existence of node does not guaranteed?
Just do a simple check if both nodes exists before running LCA.