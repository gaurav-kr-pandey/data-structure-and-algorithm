**Problem Link:** https://leetcode.com/problems/balanced-binary-tree/description/

**Problem Statement:** Given a binary tree, determine if it is **height-balanced**.

>A **height-balanced** binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

### Code:

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return height(root) != -1;
    }

    private int height(TreeNode root) {
        
        if (root == null) {
            return 0;
        }

        int lh = height(root.left);
        int rh = height(root.right); 

        if (lh == -1 || rh == -1) {
            return -1;
        }

        if (Math.abs(lh - rh) > 1) {
            return -1;
        }

        return 1 + Math.max(lh, rh);
    }
}
```