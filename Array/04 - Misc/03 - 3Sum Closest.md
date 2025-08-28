https://leetcode.com/problems/3sum-closest/description/

Given an integer array `nums` of length `n` and an integer `target`, find three integers in `nums` such that the sum is closest to `target`.
Return _the sum of the three integers_.
You may assume that each input would have exactly one solution.

### Code:

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {

        int closestSum = (int) 1e6;
        int n = nums.length;
        Arrays.sort(nums);

        for (int i = 0; i < n - 2; i++) {
            int start = i + 1;
            int end = n - 1;
            while (start < end) {
                int currentSum = nums[i] + nums[start] + nums[end];
                if (Math.abs(target - currentSum) < Math.abs(target - closestSum)) {
                    closestSum = currentSum;
                }
                if (currentSum < target) {
                    start++;
                } else if (currentSum > target){
                    end--;
                } else {
                    return closestSum;
                }
            }
        }

        return closestSum;
    }
}
```