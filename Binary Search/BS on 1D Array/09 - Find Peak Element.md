[Leetcode - Practice](https://leetcode.com/problems/find-peak-element/description/)

```java
class Solution {
    public int findPeakElement(int[] nums) {
        int low = 0, high = nums.length - 1;

		// We will not run if low == high
        while (low < high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] > nums[mid + 1]) {
                // peak is on the left (including mid)
                high = mid;
            } else {
                // peak is on the right
                low = mid + 1;
            }
        }

        return low;  // or return high; both are same here
    }
}
```