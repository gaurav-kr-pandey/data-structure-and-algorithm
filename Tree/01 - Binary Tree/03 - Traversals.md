Traversal means visiting all the nodes of the tree in a specific order.

```
	   1
	 /   \
	2     3
   / \   /
  4   5 6
```
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

**Output:** `4 2 5 1 3 6`
**Time Complexity:** $O(n)$
**Space Complexity:** $O(n)$

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

**Output:** `1 2 4 5 3 6`
**Time Complexity:** $O(n)$
**Space Complexity:** $O(n)$

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

**Output:** `4 5 2 6 3 1`
**Time Complexity:** $O(n)$ 
**Space Complexity:** $O(n)$
### 2. Breadth First Traversal (BFS)

Also known as **Level Order Traversal** (visit nodes level by level).

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

**Output:** `1 2 3 4 5 6`
**Time Complexity:** $O(n)$
**Space Complexity:** $O(n)$