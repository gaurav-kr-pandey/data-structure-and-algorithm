https://leetcode.com/problems/linked-list-cycle-ii/description/

Given the `head` of a linked list, return _the node where the cycle begins. If there is no cycle, return_ `null`.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to (**0-indexed**). It is `-1` if there is no cycle. **Note that** `pos` **is not passed as a parameter**.

**Do not modify** the linked list.

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png)

**Input:** head = [3,2,0,-4], pos = 1
**Output:** tail connects to node index 1
**Explanation:** There is a cycle in the linked list, where tail connects to the second node.

## Solution:

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        if (fast == null || fast.next == null) {
            return null;
        }

        while (fast !=null && fast.next !=null) {
            slow = slow.next;
            fast = fast.next.next;

            if (slow == fast) {
                break;
            }
        }        

        if (slow != fast) {
            return null;
        }

        fast = head;

        while (fast != slow) {
            fast = fast.next;
            slow = slow.next;
        }

        return fast;
    }
}
```