**Problem Link:** https://leetcode.com/problems/diameter-of-binary-tree/description/

**Problem Statement:**
Given the `root` of a binary tree, return _the length of the **diameter** of the tree_.
The **diameter** of a binary tree is the **length** of the longest path between any two nodes in a tree. This path may or may not pass through the `root`.
The **length** of a path between two nodes is represented by the number of edges between them.

**Example:**
**Input:** root = `[1,2,3,4,5]`
**Output:** 3
**Explanation:** 3 is the length of the path `[4,2,1,3] or [5,2,1,3]`.

![[Pasted image 20250902180516.png|200]]

### Intuition:

##### Solution: $O(n^2)$
If we observe carefully diameter with every node $(v)$, we can check height $(h_1)$ of left subtree and height $(h_2)$ of right subtree plus add 1 to it.

$d = h_1 + h_2 + 1$ 

where $d$ = diameter and we are adding 1 for current node $(v)$.

Then, we will simply traverse every node and find diameter $(d)$ for that node assuming it to be a root node and find max of all.

### Code:

```java
class Solution {
	public int diameter(TreeNode root) {
		if (root == null) {
			return 0;
		}
		
		int d1 = 1 + height(root.left) + height(root.right);
		
		int d2 = diameter(root.left);
		int d3 = diameter(root.right);
		
		return Math.max(d1, Math.max(d2, d3)); 
	}
	
    private int height(TreeNode root) {
        if (root == null) {
            return 0;
        }

        return 1 + Math.max(height(root.left), height(root.right));
    }
}
```

##### Solution: $O(n)$
We can optimise the above solution by customising `height` function above in the way that we do not explicitly need to call the `height` function for every node.
We can maintain a variable outside the height function we keep updating the value of max diameter.

- At each node, the **longest path through that node** =  
    `height(left subtree) + height(right subtree)`.
- The diameter of the whole tree = **max of all such paths**.

So we need:
1. A function to compute **height** of a node.
2. While computing height, also **track max diameter**.
3. 
We use **postorder DFS**:
3. Recursively compute left height and right height.
4. Update diameter: `max(diameter, leftHeight + rightHeight)`.
5. Return height: `1 + max(leftHeight, rightHeight)`.

#### Code:

```java
class Solution {
    int diameter = 0;

    public int diameterOfBinaryTree(TreeNode root) {
        height(root);
        return diameter;
    }

    private int height(TreeNode node) {
        if (node == null) return 0;

        int left = height(node.left);
        int right = height(node.right);

        // Update diameter at this node
        diameter = Math.max(diameter, left + right);

        // Return height of this node
        return 1 + Math.max(left, right);
    }
}
```

#### Complexity Analysis
- **Time Complexity** = `O(N)`  
    Each node is visited once, height computed in constant time.
    
- **Space Complexity** = `O(H)`
    - `H` = height of the tree (worst case `O(N)` for skewed tree, best case `O(log N)` for balanced tree).
    - No extra space except recursion stack.