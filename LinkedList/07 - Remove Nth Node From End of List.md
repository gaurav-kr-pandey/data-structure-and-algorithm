https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode temp = new ListNode(-1, head);
        ListNode curr = head;
        ListNode d = temp;

        while (curr != null && n-- > 0) {
            curr = curr.next;
        }

        while (curr != null) {
            curr = curr.next;
            temp = temp.next;
        }

        temp.next = temp.next.next;

        return d.next;
    } 
}
```

