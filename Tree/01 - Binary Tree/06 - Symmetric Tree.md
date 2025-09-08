**Problem Link:** https://leetcode.com/problems/symmetric-tree/

**Problem Statement:**
Given the `root` of a binary tree, _check whether it is a mirror of itself_ (i.e., symmetric around its center).

![[Pasted image 20250902123612.png]]

**Input:** root = `[1,2,2,3,4,4,3]`
**Output:** true
### Intuition:


### Complexity:

**Time Complexity:** $O(n)$
**Space Complexity:** $O(n)$
### Code:

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }

        return isSym(root.left, root.right);
    }

    private boolean isSym(TreeNode left, TreeNode right) {
        if (left == null && right == null) {
            return true;
        }

        if (left == null || right == null) {
            return false;
        }

        return left.val == right.val && isSym(left.left, right.right) && isSym(left.right, right.left);
    }
}
```