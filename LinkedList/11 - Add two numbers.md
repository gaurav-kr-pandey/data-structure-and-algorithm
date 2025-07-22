https://leetcode.com/problems/add-two-numbers/description/

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order**, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg)

**Input:** l1 = [2,4,3], l2 = [5,6,4]
**Output:** [7,0,8]
**Explanation:** 342 + 465 = 807

## Solution:

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {

        ListNode  res = new ListNode(-1);
        ListNode temp = res;
        int carry = 0;

        while (l1 != null || l2 != null || carry != 0) {
            int x = 0, y = 0;
            if (l1 != null) {
                x = l1.val;
                l1 = l1.next;
            }

            if (l2 != null) {
                y = l2.val;
                l2 = l2.next;
            }

            int z = (x + y + carry) % 10;
            carry = (x + y + carry) / 10;

            res.next = new ListNode(z);
            res = res.next;
        }

        return temp.next;
    }
}
```
