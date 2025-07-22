https://leetcode.com/problems/odd-even-linked-list/description/

## Solution:

```java
class Solution {
    public ListNode oddEvenList(ListNode head) {
        ListNode even = new ListNode(-1);
        ListNode odd = new ListNode(-2);
        ListNode e = even;
        ListNode o = odd;
        boolean isEven = false;

        while (head != null) {
            if (isEven) {
                even.next = head;
                even = even.next;
            } else {
                odd.next = head;
                odd = odd.next;
            }
            isEven = !isEven;
            head = head.next;
        }

        even.next = null;
        odd.next = e.next;

        return o.next;
    }
}
```