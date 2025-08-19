https://leetcode.com/problems/minimum-path-sum/description/

Given a `m x n` `grid` filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.
**Note:** You can only move either down or right at any point in time.

![[Pasted image 20250818101640.png]]

**Code:**

```java
class Solution {
    public int minPathSum(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int[][] dp = new int[m + 1][n + 1];
        for (int[] row : dp)
            Arrays.fill(row, -1);

        return helper(grid, m - 1, n - 1, dp);
    }

    private int helper(int[][] grid, int m, int n, int[][] dp) {

        if (m == 0 && n == 0) {
            return grid[m][n];
        }

        if (m < 0 || n < 0) {
            return Integer.MAX_VALUE;
        }

        if (dp[m][n] != -1) {
            return dp[m][n];
        }
        int choice1 = helper(grid, m - 1, n, dp);
        int choice2 = helper(grid, m, n - 1, dp);
        dp[m][n] = grid[m][n] + Math.min(choice1, choice2);

        return dp[m][n];
    }
}
```