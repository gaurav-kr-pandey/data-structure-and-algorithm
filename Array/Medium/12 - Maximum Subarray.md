https://leetcode.com/problems/maximum-subarray/description/

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int currSum=0; int maxSum=Integer.MIN_VALUE;

        for(int i=0; i<nums.length; i++) {
            if(currSum+nums[i]>=nums[i]) {
                currSum+=nums[i];
            } else {
                currSum = nums[i];
            }

            maxSum = Math.max(currSum, maxSum);
        }

        return maxSum;
    }
}
```