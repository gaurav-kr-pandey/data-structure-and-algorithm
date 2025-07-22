https://leetcode.com/problems/palindrome-linked-list/description/

## Solution

```java
class Solution {

    public boolean isPalindrome(ListNode head) {

        if (head == null || head.next == null) {
            return true;
        }

        ListNode temp = head;
        ListNode middle = getMiddle(temp);
        middle = reverse(middle);

        return isEquals(head, middle);

    }

    private ListNode reverse(ListNode head) {

        ListNode prev = null;

        while (head != null) {
            ListNode r = head.next;
            head.next = prev;
            prev = head;
            head = r;
        }

        return prev;
    }

    private boolean isEquals(ListNode l1, ListNode l2) {
        while (l1 != null && l2 != null) {
            if (l1.val != l2.val) {
                return false;
            }

            l1 = l1.next;
            l2 = l2.next;
        }

        return true;
    }

    private ListNode getMiddle(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }

        return slow;
    }
}
```