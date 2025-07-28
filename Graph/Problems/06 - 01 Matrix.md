https://leetcode.com/problems/01-matrix/description/
Given an `m x n` binary matrix `mat`, return _the distance of the nearest_ `0` _for each cell_.
The distance between two cells sharing a common edge is `1`.

---
**Note:**
> Exactly same problem, framed differently - https://leetcode.com/problems/map-of-highest-peak/description/
## Approach

push all the zeroes in the queue and add 1-distance at each step.

```java
class Solution {

    public int[][] updateMatrix(int[][] mat) {
        int m = mat.length, n = mat[0].length;
        Queue<int[]> q = new LinkedList<>();
        boolean[][] vis = new boolean[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (mat[i][j] == 0) {
                    q.add(new int[] { i, j });
                    vis[i][j] = true;
                }
            }
        }
        int[][] dirs = new int[][] { { 1, 0 }, { 0, 1 }, { -1, 0 }, { 0, -1 } };
        while (!q.isEmpty()) {
            boolean hasOne = false;
            int[] curr = q.poll();
            int row = curr[0];
            int col = curr[1];
            for (int[] dir : dirs) {
                int newRow = row + dir[0];
                int newCol = col + dir[1];
                if (isValid(mat, newRow, newCol) && !vis[newRow][newCol]) {
                    q.add(new int[] { newRow, newCol });
                    vis[newRow][newCol] = true;
                    mat[newRow][newCol] = mat[row][col] + 1;
                }
            }
        }
        return mat;
    }

    private boolean isValid(int[][] mat, int row, int col) {
        int m = mat.length, n = mat[0].length;
        return row >= 0 && row < m && col >= 0 && col < n && mat[row][col] == 1;
    }
}

```
