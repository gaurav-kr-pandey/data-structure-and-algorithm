
[[Binary Search/BS on 1D Array/Introduction|Introduction]]

[Practice Here](https://leetcode.com/problems/binary-search/description/)

**Code:**

```java
class Solution {
    public int search(int[] nums, int target) {
        int low  = 0, high = nums.length - 1, ans = -1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {
                return mid;
            }

            if (nums[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return -1;
    }
}
```