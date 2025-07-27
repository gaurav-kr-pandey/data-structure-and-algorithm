**Problem Statement:** Given an array and a sum k, we need to print the length of the longest subarray that sums to k.

---
> **Key observations:**
> `longest subarray`, `length`, `positive integers only`

**Approach:** Sliding window (Works only for positive numbers), this problem can also be solve using - [[02 - Longest subarray with sum k(Includes Negative)]]

Related - [[02 - Longest subarray with sum k(Includes Negative)]] , [[03 - Longest Subarray with 0 Sum (Includes Negative)]]

### Code:



```java
class Solution {
    public int subarraySum(int[] nums, int k) {
    
        int i = 0, j = 0, n = nums.length, sum = 0, maxLen = 0;

        while (j < n) {
        
            sum += nums[j];
            while (sum > k && i < j) {
                sum -= nums[i++];
            }

            if (sum == k) {
                maxLen = Math.max(maxLen, j - i + 1);
            }

            j++;
        }

        return maxLen;
    }
}
```