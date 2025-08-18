https://leetcode.com/problems/unique-paths-ii/description/

**Code:**


```java
class Solution {
    public int uniquePathsWithObstacles(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int[][] dp = new int[m + 1][n + 1];
        for (int[] row : dp)
            Arrays.fill(row, -1);
        
        return helper(grid, m - 1, n - 1, dp);
    }

    private int helper(int[][] grid, int m, int n, int[][] dp) {

        if (m < 0 || n < 0 || grid[m][n] == 1) {
            return 0;
        }

        if (m == 0 && n == 0) {
            return 1;
        }

        if (dp[m][n] != -1) {
            return dp[m][n];
        }

        dp[m][n] = helper(grid, m - 1, n, dp) + helper(grid, m, n - 1, dp);

        return dp[m][n];
    }
}
```