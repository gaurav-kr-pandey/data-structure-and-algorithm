https://leetcode.com/problems/squares-of-a-sorted-array/description/

Given an integer array `nums` sorted in **non-decreasing** order, return _an array of **the squares of each number** sorted in non-decreasing order_.

**Example 1:**
**Input:** `nums` = `[-4,-1,0,3,10]`
**Output:** `[0,1,9,16,100]`
**Explanation:** After squaring, the array becomes `[16,1,0,9,100]`.
After sorting, it becomes `[0,1,9,16,100]`.

### Code

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int n = nums.length, i = 0, j = n - 1, k = n - 1;
        int[] result = new int[n];
        while (i <= j) {
            if (nums[i] * nums[i] < nums[j] * nums[j]) {
                result[k] = nums[j] * nums[j];
                j--;
            } else {
                result[k] = nums[i] * nums[i];
                i++;
            }
            k--;
        }
        return result;
    }
}
```