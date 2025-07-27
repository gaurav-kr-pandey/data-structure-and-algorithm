https://leetcode.com/problems/rotting-oranges/

You are given an `m x n` `grid` where each cell can have one of three values:
- `0` representing an empty cell,
- `1` representing a fresh orange, or
- `2` representing a rotten orange.
Every minute, any fresh orange that is **4-directionally adjacent** to a rotten orange becomes rotten.
Return _the minimum number of minutes that must elapse until no cell has a fresh orange_. If _this is impossible, return_ `-1`.

**Example 1:**
![](https://assets.leetcode.com/uploads/2019/02/16/oranges.png)

**Input:** grid = [[2,1,1],[1,1,0],[0,1,1]]
**Output:** 4

### Solution:

```java
class Solution {

    public int orangesRotting(int[][] grid) {
        
        int m = grid.length, n = grid[0].length, fresh = 0;
        Queue<int[]> q = new LinkedList<>();
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 2) {
                    q.add(new int[] { i, j });
                } else if (grid[i][j] == 1) {
                    fresh++;
                }
            }
        }
        
        if (fresh == 0) {
            return 0;
        }
        
        int minutes = 0;
        int[][] dirs = new int[][] { { 0, 1 }, { 1, 0 }, { -1, 0 }, { 0, -1 } };
        
        while (!q.isEmpty()) {
            int size = q.size();
            boolean isRotten = false;
            while (size-- > 0) {
                int[] curr = q.poll();
                int row = curr[0];
                int col = curr[1];
                for (int[] dir : dirs) {
                    int i = row + dir[0];
                    int j = col + dir[1];
                    if (isValidMove(grid, i, j)) {
                        grid[i][j] = 2;
                        q.add(new int[] { i, j });
                        isRotten = true;
                        fresh--;
                    }
                }
            }
            if (isRotten) {
                minutes++;
            }
        }
        return fresh == 0 ? minutes : -1;
    }

    private boolean isValidMove(int[][] grid, int i, int j) {
        int m = grid.length, n = grid[0].length;
        return i >= 0 && i < m && j >= 0 && j < n && grid[i][j] == 1;
    }
}
```