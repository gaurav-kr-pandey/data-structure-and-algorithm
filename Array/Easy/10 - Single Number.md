
[practice](https://leetcode.com/problems/single-number/description/

Given a **non-empty** array of integers `nums`, every element appears _twice_ except for one. Find that single one.
You must implement a solution with a linear runtime complexity and use only constant extra space.

**Example 1:**
**Input:** nums = [2,2,1]
**Output:** 1

**Example 2:**
**Input:** nums = [4,1,2,1,2]
**Output:** 4
### Solution:

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