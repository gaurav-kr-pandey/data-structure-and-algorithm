https://leetcode.com/problems/intersection-of-two-linked-lists/description/

Given the heads of two singly linked-lists `headA` and `headB`, return _the node at which the two lists intersect_. If the two linked lists have no intersection at all, return `null`.

For example, the following two linked lists begin to intersect at node `c1`:

![](https://assets.leetcode.com/uploads/2021/03/05/160_statement.png)

The test cases are generated such that there are no cycles anywhere in the entire linked structure.

**Note** that the linked lists must **retain their original structure** after the function returns.

## Solution:


```java
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {

        if (headA == null || headB == null) {
            return headA;
        }

        ListNode x = headA;
        ListNode y = headB;

        while (x != y) {
            x = x == null ? headB : x.next;
            y = y == null ? headA : y.next;
        }

        return x;
    }
}
```