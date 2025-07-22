

[25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/)


Given the `head` of a linked list, reverse the nodes of the list `k` at a time, and return _the modified list_.

`k` is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of `k` then left-out nodes, in the end, should remain as it is.

You may not alter the values in the list's nodes, only nodes themselves may be changed.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg)

**Input:** head = [1,2,3,4,5], k = 2
**Output:** [2,1,4,3,5]

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg)

**Input:** head = [1,2,3,4,5], k = 3
**Output:** [3,2,1,4,5]

## Solution

## ✅ Approach Using Recursion

### 🔁 Steps:

1. Check if there are at least k nodes ahead.
2. If yes, reverse the first `k` nodes.
3. Make a recursive call to process the rest of the list.
4. Connect the reversed `k` nodes to the result of the recursive call.
---
## ✅ Time and Space Complexity

- **Time Complexity:** `O(n)` — each node is visited exactly once.
- **Space Complexity:** `O(n/k)` due to recursion stack in worst case (but can be seen as `O(n)` in general due to recursion depth).


```java
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
		// Step 1: Check if we have at least k nodes		
        if (!hasKLength(head, k)) {
            return head;
        }
		// Step 2: Reverse the first k nodes
        ListNode prev = null;
        ListNode curr = head;
        ListNode next = null;
        int i = 0;

        while (curr != null && i < k) {
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
            i++;
        }
		// Step 3: Recurse on the remaining list
        head.next = reverseKGroup(next, k);
		// Step 4: Return the new head after reversal (prev)
        return prev;
    }

    private boolean hasKLength(ListNode head, int k) {
        ListNode curr = head;
        int i = 0;
        while (curr != null && i < k) {
            curr = curr.next;
            i++;
        }

        return i == k;
    }
}
```
#### Example :

Input list: `1 → 2 → 3 → 4 → 5`  
`k = 3`

|Step|curr|prev|next|head|return|
|---|---|---|---|---|---|
|Call 1 Start|1|null|?|1|recurse(4)|
|Iter 1|2|1|2|||
|Iter 2|3|2|3|||
|Iter 3|4|3|4|||
|Call 2 Start|4|null|?|4|return 4|
|Final Link||||1.next = 4|return 3 (new head)|