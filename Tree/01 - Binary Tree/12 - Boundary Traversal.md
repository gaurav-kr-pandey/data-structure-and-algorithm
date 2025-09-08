**Problem Link:** [GeeksforGeeks - Boundary Traversal](https://www.geeksforgeeks.org/problems/boundary-traversal-of-binary-tree/1)

---
## Problem
Given a binary tree, return its **boundary traversal** in anti-clockwise direction starting from the root.  
The boundary includes:
1. Root node
2. Left boundary (excluding leaves)
3. All leaf nodes (left to right)
4. Right boundary (excluding leaves, added in reverse)

---
## Possible Solutions

### 1. BFS / Level Order Approach
- Traverse level by level.
- Pick leftmost and rightmost non-leaf nodes, plus leaves.
- Merge lists for final answer.

**Complexity:**  
- Time: `O(N)`  
- Space: `O(N)` (queue + lists)  
⚠️ Issue: Fails in skewed trees (not always correct boundary).

---
### 2. DFS with Separate Functions ✅ (Optimal)
- Add root (if not leaf).
- Traverse left boundary: go left if exists, else right.
- Traverse leaves: DFS entire tree, add leaf nodes.
- Traverse right boundary: go right if exists, else left, store in stack, then reverse.

**Complexity:**  
- Time: `O(N)` (each node visited once).  
- Space: `O(H)` recursion + `O(H)` stack for right boundary (where `H` = height of tree).  
- ✅ Works for skewed and balanced trees.

---

## Observation & Intuition
- Root must be handled carefully (avoid duplication if root is also a leaf).  
- Left boundary: always follow left if possible, else right.  
- Right boundary: always follow right if possible, else left, and reverse order.  
- Leaves: add during DFS traversal.  
- Splitting logic into 3 parts (`left`, `leaves`, `right`) makes the implementation clean and avoids edge case hacks.

---

## Optimal Code (Java)

```java
class Solution {
    public ArrayList<Integer> boundaryTraversal(Node node) {
        ArrayList<Integer> res = new ArrayList<>();
        if (node == null) return res;

        // Add root (if not leaf)
        if (!isLeafNode(node)) res.add(node.data);

        // Left boundary
        addLeftBoundary(node.left, res);

        // Leaves
        addBottomBoundary(node, res);

        // Right boundary
        addRightBoundary(node.right, res);

        return res;
    }

    private void addLeftBoundary(Node node, ArrayList<Integer> list) {
        while (node != null) {
            if (!isLeafNode(node)) list.add(node.data);
            node = (node.left != null) ? node.left : node.right;
        }
    }

    private void addBottomBoundary(Node node, ArrayList<Integer> list) {
        if (node == null) return;
        if (isLeafNode(node)) {
            list.add(node.data);
            return;
        }
        addBottomBoundary(node.left, list);
        addBottomBoundary(node.right, list);
    }

    private void addRightBoundary(Node node, ArrayList<Integer> list) {
        Stack<Integer> stack = new Stack<>();
        while (node != null) {
            if (!isLeafNode(node)) stack.push(node.data);
            node = (node.right != null) ? node.right : node.left;
        }
        while (!stack.isEmpty()) list.add(stack.pop());
    }

    private boolean isLeafNode(Node curr) {
        return curr.left == null && curr.right == null;
    }
}
```

