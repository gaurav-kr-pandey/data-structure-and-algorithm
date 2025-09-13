https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(-1, head);
        ListNode curr = head;
        ListNode result = dummy;

        while (n-- > 0 && curr != null) {
            curr = curr.next;
        }

        while (curr != null) {
            dummy = dummy.next;
            curr = curr.next;
        }

        dummy.next = dummy.next.next;

        return result.next;
    }
}
```

