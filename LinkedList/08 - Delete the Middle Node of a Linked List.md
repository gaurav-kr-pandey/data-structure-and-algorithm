https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/description/

```java
class Solution {
    public ListNode deleteMiddle(ListNode head) {
        ListNode dummy = new ListNode(-1, head);
        ListNode slow = dummy;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        } 

        slow.next = slow.next.next;

        return dummy.next;
    }
}
```