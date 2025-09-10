https://www.geeksforgeeks.org/problems/root-to-leaf-paths/1

Given a **Binary Tree**, you need to **find all the possible paths** from the **root node** to all the **leaf nodes** of the binary tree.

**Note:** The paths should be returned such that paths from the left subtree of any node are **listed first**, followed by paths from the right subtree.

**Examples:**
**Input:** `root[] = [1, 2, 3, 4, 5, N, N]`

![[Pasted image 20250910194539.png|250]]

**Output:** `[[1, 2, 4], [1, 2, 5], [1, 3]]`
**Explanation:** All the possible paths from root node to leaf nodes are: 
`[1 -> 2 -> 4], [1 -> 2 -> 5], [1 -> 3]`

## Intuition:
 
The problem asks for all paths from the root to every leaf in a binary tree. A **preorder traversal** (Root-Left-Right) is a natural fit for this problem. We can explore the tree from the root, and for each node, we add it to a temporary list that represents the current path. When we reach a leaf node (a node with no children), we know we've found a complete path from the root to a leaf. We then add a copy of our temporary list to our final result. After visiting a node and its children, we need to **backtrack** by removing the current node from our temporary list. This ensures that when we explore other branches of the tree, our path list is accurate.  
  
## Complexity:

* **Time Complexity**: O(N), where N is the number of nodes in the tree. We visit each node in the tree exactly once.  
* **Space Complexity**: O(H), where H is the height of the tree. This is because of the recursion stack. In the worst-case scenario (a skewed tree), the height of the tree can be N, leading to a space complexity of O(N).  
  
## Code:

```java  
class Solution {  
    public static List<List<Integer>> Paths(Node root) {  
        List<ArrayList<Integer>> res = new ArrayList<>();  
        preorder(root, res, new ArrayList<>());  
        return res;  
    }  
  
    private static void preorder(Node root, List<List<Integer>> res, List<Integer> list) {  
  
        if (root == null) {  
            return;  
        }  
  
        list.add(root.data);  
  
        if (root.left == null && root.right == null) {  
            res.add(new ArrayList<>(list));  
        }  
  
        preorder(root.left, res, list);  
        preorder(root.right, res, list);  
  
        list.remove(list.size() - 1);  
    }  
}  
```