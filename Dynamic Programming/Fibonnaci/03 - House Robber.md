https://leetcode.com/problems/house-robber/description/

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security systems connected and **it will automatically contact the police if two adjacent houses were broken into on the same night**.
Given an integer array `nums` representing the amount of money of each house, return _the maximum amount of money you can rob tonight **without alerting the police**_.


**Code:**

```java
class Solution {

    public int rob(int[] nums) {
        int n = nums.length;

        int[] dp = new int[n + 1];

        Arrays.fill(dp, -1);

        return rob(nums, n - 1, dp);
    }

    public int rob(int[] nums, int i, int[] dp) {
        int n = nums.length;

        if (i < 0) {
            return 0;
        }

        if (dp[i] != -1) {
            return dp[i];
        }

        dp[i] = Math.max(nums[i] + rob(nums, i - 2, dp), rob(nums, i - 1, dp));

        return dp[i];
    }
}

```