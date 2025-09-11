https://www.geeksforgeeks.org/problems/children-sum-parent/1

Given the **root** of a binary tree, determine whether the tree satisfies the **Children Sum Property**. In this property, each non-leaf node must have a value equal to the **sum** of its **left** and **right** children's values. A NULL child is considered to have a value of **0**, and all leaf nodes are considered valid by default.  
Return **true** if every node in the tree satisfies this condition, otherwise return **false**.

**Examples:**

**Input:** `root = [35, 20, 15, 15, 5, 10, 5]`

![|250](https://media.geeksforgeeks.org/img-practice/prod/addEditProblem/907368/Web/Other/blobid1_1754457377.webp)
**Output:** True
**Explanation:** Here, every node is sum of its left and right child.

### Code:

```java
class Solution {
    public boolean isSumProperty(Node root) {
        // Empty tree satisfies property
        if (root == null) {
            return true;
        }

        // Edge Case: Leaf node always satisfies property
        if (root.left == null && root.right == null) {
            return true;
        }

        int sum = 0;
        if (root.left != null) sum += root.left.data;
        if (root.right != null) sum += root.right.data;

        return root.data == sum 
            && isSumProperty(root.left) 
            && isSumProperty(root.right);
    }
}
```