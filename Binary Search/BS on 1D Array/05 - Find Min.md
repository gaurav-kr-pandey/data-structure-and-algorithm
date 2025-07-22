[Leetcode - Practice](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)


```java
class Solution {
    public int findMin(int[] nums) {
        int low = 0, high = nums.length - 1, min = Integer.MAX_VALUE;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] > nums[high]) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }

            min = Math.min(nums[mid], min);
        }

        return min;
    }
}
```