https://leetcode.com/problems/number-of-islands/

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return _the number of islands_.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

**Input:** 
grid = 
```java
[
  ["1","1","1","1","0"],
  ["1","1","0","1","0"],
  ["1","1","0","0","0"],
  ["0","0","0","0","0"]
]
```
**Output:** 1

## Code:

**DFS Based :**
```java
class Solution {
    public int numIslands(char[][] grid) {

        int m = grid.length, n = grid[0].length, islands = 0;

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (isValidMove(grid, i, j)) {
                    dfs(grid, i, j);
                    islands++;
                }
            }
        }

        return islands;
    }

    private void dfs(char[][] grid, int row, int col) {
        if (!isValidMove(grid, row, col)) return;

        grid[row][col] = '0';

        dfs(grid, row, col + 1);
        dfs(grid, row, col - 1);
        dfs(grid, row - 1, col);
        dfs(grid, row + 1, col);
    }

    private boolean isValidMove(char[][] grid, int row, int col) {
        int m = grid.length, n = grid[0].length;
        return row >= 0 && row < m && col >= 0 && col < n && grid[row][col] == '1';
    }
}
```

**BFS Based :**
```java
class Solution {

    class Cell {

        int row;
        int col;
        Cell(int row, int col) {
            this.row = row;
            this.col = col;
        }

        public List<Cell> getAdjacentCells(char[][] grid) {
            List<Cell> adj = new ArrayList<>();

            if (isValidCell(grid, row + 1, col)) {
                adj.add(new Cell(row + 1, col));
            }
            if (isValidCell(grid, row - 1, col)) {
                adj.add(new Cell(row - 1, col));
            }
            if (isValidCell(grid, row, col + 1)) {
                adj.add(new Cell(row, col + 1));
            }
            if (isValidCell(grid, row, col - 1)) {
                adj.add(new Cell(row, col - 1));
            }

            return adj;
        }

        private boolean isValidCell(char[][] grid, int row, int col) {
            return (
                row < grid.length &&
                row > -1 &&
                col < grid[0].length &&
                col > -1 &&
                grid[row][col] == '1'
            );
        }

        public int getRow() {
            return this.row;
        }

        public int getCol() {
            return this.col;
        }
    }

    public int numIslands(char[][] grid) {
        int count = 0;

        for (int row = 0; row < grid.length; row++) {
            for (int col = 0; col < grid[0].length; col++) {
                if (grid[row][col] == '1') {
                    bfs(grid, row, col);
                    count++;
                }
            }
        }

        return count;
    }

    private void bfs(char[][] grid, int uRow, int uCol) {
        Queue<Cell> q = new LinkedList<>();
        q.add(new Cell(uRow, uCol));
        grid[uRow][uCol] = '0';

        while (!q.isEmpty()) {
            Cell u = q.poll();
            for (Cell v : u.getAdjacentCells(grid)) {
                int vRow = v.getRow();
                int vCol = v.getCol();
                q.add(new Cell(vRow, vCol));
                grid[vRow][vCol] = '0';
            }
        }
    }
}
```