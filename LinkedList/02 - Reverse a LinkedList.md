https://leetcode.com/problems/reverse-linked-list/description/

Given the `head` of a singly linked list, reverse the list, and return _the reversed list_.

```java
class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode temp = head;
        while (temp != null) {
            ListNode right = temp.next;
            temp.next = prev;
            prev = temp;
            temp = right;
        }

        return prev;
    }
}
```
