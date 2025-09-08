**Problem Link:** https://leetcode.com/problems/maximum-depth-of-binary-tree/description/

**Problem Statement:**
Given the `root` of a binary tree, return _its maximum depth_.
A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.
### Intuition:


### Complexity:

**Time Complexity:** $O(n)$
**Space Complexity:** $O(n)$
### Code:

```java
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }

        int left = 1 + maxDepth(root.left);
        int right = 1 + maxDepth(root.right);

        return Math.max(left, right);
    }
}
```

