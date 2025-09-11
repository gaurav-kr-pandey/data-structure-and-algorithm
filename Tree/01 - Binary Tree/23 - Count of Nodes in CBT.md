https://leetcode.com/problems/count-complete-tree-nodes/

Given the `root` of a **complete** binary tree, return the number of the nodes in the tree.
According to **[Wikipedia](http://en.wikipedia.org/wiki/Binary_tree#Types_of_binary_trees)**, every level, except possibly the last, is completely filled in a complete binary tree, and all nodes in the last level are as far left as possible. It can have between `1` and `2h` nodes inclusive at the last level `h`.
Design an algorithm that runs in less than `O(n)` time complexity.

## Code:

```java
class Solution {
    public int countNodes(TreeNode root) {
        if (root == null) {
            return 0;
        }

        return 1 + countNodes(root.left) +countNodes(root.right);
    }
}
```