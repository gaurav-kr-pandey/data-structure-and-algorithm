https://leetcode.com/problems/sort-list/description/

```java
class Solution {
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode middle = getMiddle(head);
        ListNode left = head;
        ListNode right = middle;

        ListNode l1 = sortList(left);
        ListNode l2 = sortList(right);

        return mergeSortedList(l1, l2);
    }

    private ListNode getMiddle(ListNode head) {
        ListNode prev = null;
        ListNode slow = head;
        ListNode fast = head;

        while (fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }

        if (prev != null) {
            prev.next = null;
        }

        return slow;
    }

    private ListNode mergeSortedList(ListNode l1, ListNode l2) {
        if (l1 == null && l2 == null) {
            return null;
        }

        if (l1 == null) {
            return l2;
        }

        if (l2 == null) {
            return l1;
        }

        ListNode dummy = new ListNode(-1);
        ListNode head =  dummy;

        while (l1 != null && l2 != null) {
            if (l1.val > l2.val) {
                dummy.next = l2;
                l2 = l2.next;
            } else {
                dummy.next = l1;
                l1 = l1.next;
            }
            dummy = dummy.next;
        }

        if (l1 == null) {
            dummy.next = l2;
        }

        if (l2 == null) {
            dummy.next = l1;
        }

        return head.next;
    }
}
```