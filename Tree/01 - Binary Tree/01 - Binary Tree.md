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
# Tree Traversals
Traversal means visiting all the nodes of the tree in a specific order.
### 1. Depth First Traversals (DFS)

**Inorder (Left → Root → Right)**

```java
public void inOrder(TreeNode root) {
	if (root == null) {
		return;
	}
	
	inOrder(root.left);
	System.out.print(root.val);
	inOrder(root.right);
}
```

**Preorder (Root → Left → Right)**

```java
public void preOrder(TreeNode root) {
	if (root == null) {
		return;
	}
	
	System.out.print(root.val);
	preOrder(root.left);
	preOrder(root.right);
}
```

**Postorder (Left → Right → Root)**

```java
public void preOrder(TreeNode root) {
	if (root == null) {
		return;
	}
	
	preOrder(root.left);
	preOrder(root.right);
	System.out.print(root.val);
}
```

### 2. Breadth First Traversal (BFS)
- Also known as **Level Order Traversal** (visit nodes level by level).

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
    
        List<List<Integer>> res = new ArrayList<>();
        if(root == null) 
	        return res;
        
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        
        while(!q.isEmpty()) {
            int size = q.size();
            List<Integer> list = new ArrayList<>(size);
            
            while(size-- > 0) {
                TreeNode curr = q.poll();
                list.add(curr.val);
    
                if(curr.left != null) 
                    q.add(curr.left);
                if(curr.right != null)
                    q.add(curr.right);
            }
            res.add(list);
        }
        
        return res;
    }
}
```
---

## Examples

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