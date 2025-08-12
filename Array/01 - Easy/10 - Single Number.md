
[practice](https://leetcode.com/problems/single-number/description/

Given a **non-empty** array of integers `nums`, every element appears _twice_ except for one. Find that single one.
You must implement a solution with a linear runtime complexity and use only constant extra space.

**Example 1:**
**Input:** nums = [2,2,1]
**Output:** 1

**Example 2:**
**Input:** nums = [4,1,2,1,2]
**Output:** 4
### Intuition:

We can start thinking by *Brute Force* in which we can use two loops $i....n$ and a nested $j = i + 1....n$ 

```java
for (i = 0; i < n; i++) {
	for (j = i + 1; j < n; j++) {
	}
}
```

But the time complexity of two loops will be O($n^2$). Can we optimise it even further?
Yes, we can maintain a frequency map but in that case we will be using extra space and space complexity will be O($n$).

**Optimal Solution:** Think in terms of two numbers canceling out each other and if there is any number that does not cancel out remains our answer.

*Does this sound like XOR operation?*
Yes, we will be using XOR operation to solve this in O($n$) time complexity without using any extra space. To Know more about XOR you can visit this document - [[02 - Introduction - XOR]]

*Why it works:*
`(a ^ a) ^ (b ^ b) ^ (c) = 0 ^ 0 ^ c => c`

**Code:**

```java
class Solution {
    public int singleNumber(int[] nums) {
        int num = nums[0];

        for (int i = 1; i < nums.length; i++) {
            num = num ^ nums[i];
        }

        return num;
    }
}
```