[Leetcode 1248 - Practice](https://leetcode.com/problems/count-number-of-nice-subarrays/description/)

Given an array of integers `nums` and an integer `k`. A continuous subarray is called **nice** if there are `k` odd numbers on it.

Return _the number of **nice** sub-arrays_.

**Example 1:**

**Input:** nums = [1,1,2,1,1], k = 3
**Output:** 2
**Explanation:** The only sub-arrays with 3 odd numbers are [1,1,2,1] and [1,2,1,1].

## Solution

```java
class Solution {
    public int numberOfSubarrays(int[] nums, int k) {
        int oddCount = 0, n = nums.length, niceSubarrays = 0;
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);

        for (int i = 0; i < n; i++) {
            if (nums[i] % 2 != 0) {
                oddCount++;
            }

            niceSubarrays += map.getOrDefault(oddCount - k, 0);
            map.put(oddCount, map.getOrDefault(oddCount, 0) + 1);
        }

        return niceSubarrays;
    }
}
```