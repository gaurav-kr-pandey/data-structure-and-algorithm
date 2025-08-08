[practice](https://leetcode.com/problems/missing-number/description/)

Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return _the only number in the range that is missing from the array._

**Example 1:**
**Input:** nums = [3,0,1]
**Output:** 2
**Explanation:** `n = 3` since there are 3 numbers, so all numbers are in the range `[0,3]`. 2 is the missing number in the range since it does not appear in `nums`.

### Solution:

```java
class Solution {
    public int missingNumber(int[] nums) {

        int n = nums.length;
        int totalSum = 0;

        for(int x : nums) {
            totalSum += x;
        }
            
        int sum = n * (n + 1) / 2;
        return sum - totalSum;
    }
}
```