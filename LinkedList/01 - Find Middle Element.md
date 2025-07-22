https://leetcode.com/problems/middle-of-the-linked-list/description/

Given the `head` of a singly linked list, return _the middle node of the linked list_.

If there are two middle nodes, return **the second middle** node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)

**Input:** head = [1,2,3,4,5]
**Output:** [3,4,5]
**Explanation:** The middle node of the list is node 3.

## Solution:

**Algo: Tortoise Method (Fast and slow pointer)**

```java
class Solution {
    public ListNode middleNode(ListNode head) {
        if (head == null) {
            return null;
        }

        ListNode fast  = head;
        ListNode slow = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;
    }
}
```