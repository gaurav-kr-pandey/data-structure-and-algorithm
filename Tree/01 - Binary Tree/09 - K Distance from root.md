https://www.geeksforgeeks.org/problems/k-distance-from-root/1

Given a binary tree having **n** nodes and an integer **k**. Print all nodes that are at distance k from the root (root is considered at distance 0 from itself). Nodes should be printed from **left to right**.


### Code:

```java
class Tree {
    private ArrayList<Integer> list;
    public ArrayList<Integer> Kdistance(Node root, int k) {
	    
        if (list == null) {
            list = new ArrayList<>();
        }
    
        if (root == null) {
            return list;
        }
        
        Kdistance(root.left, k - 1);
        
        if (k == 0) {
            list.add(root.data);
        }
        
        
        Kdistance(root.right, k - 1);
        
        return list;
    }
}
```