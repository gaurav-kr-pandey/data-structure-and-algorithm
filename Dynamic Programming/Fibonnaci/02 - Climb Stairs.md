You are climbing a staircase. It takes `n` steps to reach the top.
Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?
https://leetcode.com/problems/climbing-stairs/description/

**Code:**


```java
class Solution {
    public int climbStairs(int n) {
        int[] dp = new int[n + 1];
        Arrays.fill(dp, -1);
        return cs(n, dp);
    }

    public int cs(int n, int[] dp) {

        if (n <= 0) {
            return 0;
        }

        if (n <= 2) {
            return n;
        }

        if (dp[n] != -1) {
            return dp[n];
        }

        dp[n] = cs(n - 1, dp) + cs(n - 2, dp);

        return dp[n];
    }
}
```