https://leetcode.com/problems/max-consecutive-ones-iii/description/

Given a binary array `nums` and an integer `k`, return _the maximum number of consecutive_ `1`_'s in the array if you can flip at most_ `k` `0`'s.

**Example 1:**

**Input:** nums = [1,  1, 1, 0, 0, 0, 1, 1, 1, 1, 0], k = 2
**Output:** 6
**Explanation:** [1, 1, 1, 0, 0, 1, 1, 1, 1, 1, 1]
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.

### Solution:

```java
class Solution {

    public int longestOnes(int[] nums, int k) {
    
        int i = 0, j = 0, n = nums.length, zeroes = 0, max = 0;
        while (j < n) {
            if (nums[j] == 0) {
                zeroes++;
            }
            while (zeroes > k) {
                if (nums[i] == 0) {
                    zeroes--;
                }
                i++;
            }
            max = Math.max(max, j - i + 1);
            j++;
        }
        return max;
    }
}

```

