
## 1. Root-to-Leaf Problems

##### 1.1 Maximum / Minimum Depth
- **Max Depth**: Height of tree.
- **Approach**: DFS recursion (`return 1 + max(left, right)`).
- **TC**: $O(n)$, **SC**: $O(h)$ `[recursion stack]`.

##### 1.2 Root-to-Leaf Path Sum
- Check if a path from root to leaf equals given sum.
- **Approach**: DFS recursion, subtract node value along path.
- **TC**: $O(n)$.

##### 1.3 All Root-to-Leaf Paths
- Collect all paths from root to leaves.
- **Approach**: Backtracking with DFS.
- **TC**: $O(n^²)$ (n paths, each up to length n in skewed).

---
## 2. Traversal-Based Patterns

##### 2.1 Iterative Traversals
- Inorder, Preorder, Postorder using stack(s).
- **TC**: $O(n)$, **SC**: $O(h)$.

##### 2.2 Level Order Variants
- Simple BFS, reverse level order, zig-zag (spiral).
- **TC**: $O(n)$, **SC**: $O(n)$ (`queue`).

---

## 3. Lowest Common Ancestor (LCA)
- Given two nodes, find their lowest common ancestor.
- **Approach**:  
  - **Recursive DFS**:
    - If root == p or root == q, return root.
    - Recurse left and right.  
    - If both sides return non-null → current root is LCA.  
- **TC**: $O(n)$, **SC**: $O(h)$.

---

## 4. Diameter of a Binary Tree
- Longest path between any 2 nodes.
- **Approach**: DFS returning height, compute `leftHeight + rightHeight` at each node.
- **TC**: $O(n)$, **SC**: $O(h)$.

---

## 5. Symmetry / Mirror Problems
- Check if a tree is symmetric (left and right subtrees mirror).
- **Approach**: Compare left vs right recursively.
- **TC**: $O(n)$.

---
## 6. Views of a Tree
- **Left View**: First node at each level (BFS/DFS).  
- **Right View**: Last node at each level.  
- **Top View**: Nodes visible from above → BFS with horizontal distance map.  
- **Bottom View**: Last nodes seen at each horizontal distance.  
- **TC**: $O(n)$, **SC**: $O(n)$.

---

## 7. Vertical Order Traversal
- Group nodes by horizontal distance from root.
- **Approach**: BFS/DFS with column index.
- **TC**: $O(n * log_2 n)$ (sorting by column), **SC**: $O(n)$.

---

## 8. Boundary Traversal
- Print boundary nodes in anticlockwise:  
  - Root → Left boundary → Leaves → Right boundary (bottom-up).
- **TC**: $O(n)$.

---

## 9. Path Problems
### 9.1 Path Sum II
- Find all root-to-leaf paths with sum = target.
- **Approach**: DFS + Backtracking.
- **TC**: $O(n²)$.

### 9.2 Maximum Path Sum
- Path can start and end at any node.
- **Approach**: DFS with “max sum at this node” tracking.
- **TC**: $O(n)$.

---

## 10. Construct Tree from Traversals
- Given:
  - **Preorder + Inorder**
  - **Postorder + Inorder**
- Use recursion with index maps.
- **TC**: $O(n)$, **SC**: $O(n)$.

---

## 11. Binary Search Tree (BST) Specific
- **Validate BST** (min-max range recursion).
- **Kth Smallest / Largest** (inorder traversal).
- **Lowest Common Ancestor in BST** (binary search property).
- **TC**: $O(h)$ avg, $O(n)$ worst.

---

## 12. Serialization & Deserialization
- Convert tree → string (BFS or Preorder with null markers).  
- Deserialize back.  
- Common in system design & LeetCode hard.  
- **TC**: $O(n)$.

---

# Quick Reference Table

| Pattern                      | Approach            | Time Complexity | Space Complexity |
|------------------------------|---------------------|----------------|-----------------|
| Max/Min Depth                | DFS                 | O(n)           | O(h)            |
| Root-to-Leaf Path Sum        | DFS                 | O(n)           | O(h)            |
| All Root-to-Leaf Paths       | DFS + Backtracking  | O(n²)          | O(h)            |
| Traversals (DFS/BFS)         | Stack/Queue         | O(n)           | O(h)/O(n)       |
| Lowest Common Ancestor       | DFS                 | O(n)           | O(h)            |
| Diameter                     | DFS                 | O(n)           | O(h)            |
| Symmetric/Mirror             | DFS/BFS             | O(n)           | O(h)            |
| Tree Views (Left/Right/Top)  | BFS + Map           | O(n)           | O(n)            |
| Vertical Order Traversal     | BFS + Map + Sort    | O(n log n)     | O(n)            |
| Boundary Traversal           | DFS/BFS             | O(n)           | O(h)            |
| Path Sum II                  | DFS + Backtracking  | O(n²)          | O(h)            |
| Max Path Sum                 | DFS                 | O(n)           | O(h)            |
| Build from Traversals        | Recursion + HashMap | O(n)           | O(n)            |
| BST Validate / Kth Smallest  | Inorder / Recursion | O(n)           | O(h)            |
| Serialize / Deserialize      | BFS/DFS             | O(n)           | O(n)            |

---
# Interview Checklist
✅ Understand traversal variants (DFS, BFS, zig-zag, views).  
✅ Practice recursive + iterative solutions.  
✅ Master LCA, Diameter, Path Sum, Max Path Sum.  
✅ Learn construction from traversals.  
✅ Revise BST-specific problems.  
✅ Be comfortable with serialization.  
