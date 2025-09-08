https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/description/

Given the `root` of a binary tree, return _the zigzag level order traversal of its nodes' values_. (i.e., from left to right, then right to left for the next level and alternate between).

**Input:** root = `[3,9,20,null,null,15,7]`
**Output:** `[[3],[20,9],[15,7]]`
### Code:

```java
class Solution {
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {

        boolean isEven = true;
        List<List<Integer>> list = new ArrayList<>();
        if (root == null) {
            return list;
        }
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);

        while (!q.isEmpty()) {

            int size = q.size();
            List<Integer> level = new ArrayList<>();
            while (size-- > 0) {
                TreeNode curr = q.poll();
                level.add(curr.val);

                if (curr.left != null) {
                    q.add(curr.left);
                }

                if (curr.right != null) {
                    q.add(curr.right);
                }
            }
            if (!isEven) {
                Collections.reverse(level);
            }

            isEven = !isEven;
            list.add(level);
        }

        return list;
    }
}
```