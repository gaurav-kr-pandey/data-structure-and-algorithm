[practice](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/description/)

Given an array `nums`, return `true` _if the array was originally sorted in non-decreasing order, then rotated **some** number of positions (including zero)_. Otherwise, return `false`.

There may be **duplicates** in the original array.

### Solution:

```java
class Solution {
    public boolean check(int[] nums) {

        int count = 0, n = nums.length;

        for (int i = 0; i < n; i++) {

            if (nums[i] > nums[(i + 1) % n]) {
                count++;
            }

            if (count > 1) {
                return false;
            }
        }

        return true;
    }
}
```