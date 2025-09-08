## What is a Binary Tree?

A **Binary Tree** is a hierarchical data structure in which each node has at most **two children**. These children are referred to as:
- **Left child**
- **Right child**
### Properties of a Binary Tree:
1. The maximum number of nodes at level `l` = $2^l$
2. Maximum number of nodes in a binary tree of height `h` = `(2^(h+1)) - 1`
3. Minimum number of nodes in a binary tree of height `h` = h + 1 (skewed tree)
4. Height of a binary tree with `n` nodes = $O(log * n)$ in the best case (balanced), $O(n)$ in the worst case (skewed).

---
## Types of Binary Trees
1. **Full Binary Tree**: Every node has 0 or 2 children.
2. **Perfect Binary Tree**: All internal nodes have 2 children and all leaves are at the same level.
3. **Complete Binary Tree**: All levels are completely filled except possibly the last, which is filled from left to right.
4. **Skewed Binary Tree**: All nodes have only one child (either left or right).

---
# Tree Traversal Examples

```
	   1
	 /   \
	2     3
   / \   /
  4   5 6
```

### Traversal Results
- **Inorder (L → Root → R):** 4 2 5 1 3 6
- **Preorder (Root → L → R):** 1 2 4 5 3 6
- **Postorder (L → R → Root):** 4 5 2 6 3 1
- **Level Order (BFS):** 1 2 3 4 5 6

---
## Applications of Binary Trees
1. Hierarchical data representation (e.g., organization structures, file systems).
2. Expression trees (used in compilers).
3. Binary Search Tree (efficient searching, insertion, and deletion).
4. Heap (used in priority queues).