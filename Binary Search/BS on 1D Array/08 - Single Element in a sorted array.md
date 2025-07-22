
You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.

Return _the single element that appears only once_.

Your solution must run in `O(log n)` time and `O(1)` space.

**Example 1:**

**Input:** nums = [1,1,2,3,3,4,4,8,8]
**Output:** 2

**Example 2:**

**Input:** nums = [3,3,7,7,10,11,11]
**Output:** 10

**Constraints:**

- `1 <= nums.length <= 105`
- `0 <= nums[i] <= 105`

## Solution:



```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int low = 0, high = nums.length - 1;

        // Edge case: only one element
        if (nums.length == 1) return nums[0];

        while (low < high) {
            int mid = low + (high - low) / 2;

            // Ensure mid is even for pairing
            if (mid % 2 == 1) mid--;

            // Check pair: mid and mid+1
            if (nums[mid] == nums[mid + 1]) {
                low = mid + 2;
            } else {
                high = mid;
            }
        }

        return nums[low];
    }
}
```
