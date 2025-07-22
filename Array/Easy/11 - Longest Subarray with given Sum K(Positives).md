**Problem Statement:** Given an array and a sum k, we need to print the length of the longest subarray that sums to k.

**Approach:** Sliding window (Works only for positive numbers)

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
    
        int i = 0, j = 0, n = nums.length, sum = 0, longest = 0;

        while (j < n) {
        
            sum += nums[j];
            while (sum > k && i < j) {
                sum -= nums[i++];
            }

            if (sum == k) {
                longest = Math.max(longest, j - i + 1);
            }

            j++;
        }

        return longest;
    }
}
```