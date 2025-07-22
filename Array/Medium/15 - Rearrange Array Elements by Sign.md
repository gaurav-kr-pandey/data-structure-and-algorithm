https://leetcode.com/problems/rearrange-array-elements-by-sign/description/

```java
class Solution {
    public int[] rearrangeArray(int[] nums) {
        int i = 0, j = 1, k = 0, n = nums.length;
        int[] res = new int[n];

        if (n == 1) {
            return nums;
        }

        while (k < n) {
            if (nums[k] < 0) {
                res[j] = nums[k];
                j = j + 2;
            } else {
                res[i] = nums[k];
                i = i + 2;
            }
            k++;
        }

        //res[n - 1] = nums[k];

        return res;
    }
}
```