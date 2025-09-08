https://leetcode.com/problems/binary-tree-maximum-path-sum/description/

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.
The **path sum** of a path is the sum of the node's values in the path.
Given the `root` of a binary tree, return _the maximum **path sum** of any **non-empty** path_.

Example:

![[Pasted image 20250902223749.png|250]]

**Input:** root = `[-10,9,20,null,null,15,7]`
**Output:** 42
**Explanation:** The optimal path is 15 $\to$ 20 $\to$ 7 with a path sum of 15 + 20 + 7 = 42.

### Key Idea

At each node:
- There are 2 cases for using this node in a path:
    1. **Return upward to parent:**  
        We can only extend **one side** (either left or right), because path cannot “branch upward”.
        `return max(left, right) + node.val`
    2. **Update global max (best path through this node):**  
        Here we can use **both children + node value**.
        `maxPath = max(maxPath, left + right + node.val)`
        
⚠️ Important: If a subtree’s contribution is **negative**, we should **ignore it** (take 0).

---

### Approach (DFS with Postorder)

1. Traverse left and right recursively.
2. Get max contributions from left and right (`max(0, dfs(child))`).
3. Update global answer: `max(global, left + right + node.val)`.
4. Return to parent: `node.val + max(left, right)`.

### Code:

```java
class Solution {
    int maxSum = Integer.MIN_VALUE;

    public int maxPathSum(TreeNode root) {
        sum(root);
        return maxSum;
    }

    public int sum(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = Math.max(0, sum(root.left));
        int right = Math.max(0, sum(root.right));

        int currSum = left + right + root.val;

        maxSum = Math.max(currSum, maxSum);

        return root.val + Math.max(left, right);
    }
}
```