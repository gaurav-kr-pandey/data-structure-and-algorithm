https://leetcode.com/problems/flood-fill/

## Intuition

The **Flood Fill** algorithm is used to fill all **connected pixels** (4-directionally) starting from a source pixel, which have the **same original color**, with a **new color**.
Think of it like a paint bucket in MS Paint: you click on a pixel and it fills all adjacent (up, down, left, right) similar-colored pixels with the new color.
We use **Breadth-First Search (BFS)** to avoid stack overflow (as in DFS) and process each pixel **level by level**.

---

## Logic Summary

1. **Check base case**: If starting pixel is already of target color → return image.
2. **Initialize BFS queue** starting from `(sr, sc)` and store the `originalColor`.
3. Traverse the grid in 4 directions.
4. For each valid neighbor (within bounds and having `originalColor`), enqueue it.
5. As we process a pixel, recolor it to avoid revisiting.

---

## Code:

```java
class Solution {
    public int[][] floodFill(int[][] image, int sr, int sc, int color) {
        // Get original color of the starting pixel
        int originalColor = image[sr][sc];
        
        // If the pixel is already of the target color, no need to process
        if (originalColor == color) return image;

        int m = image.length, n = image[0].length;

        // 4 possible directions: down, right, up, left
        int[][] dirs = {{1, 0}, {0, 1}, {-1, 0}, {0, -1}};

        // Queue for BFS traversal
        Queue<int[]> q = new LinkedList<>();
        q.add(new int[] {sr, sc});

        // BFS begins
        while (!q.isEmpty()) {
            int[] curr = q.poll();
            int row = curr[0];
            int col = curr[1];

            // Change color of current pixel
            image[row][col] = color;

            // Check all 4 neighboring cells
            for (int[] dir : dirs) {
                int newRow = row + dir[0];
                int newCol = col + dir[1];

                // If neighbor is valid and has the original color, enqueue it
                if (isValid(image, newRow, newCol, originalColor)) {
                    q.add(new int[] {newRow, newCol});
                }
            }
        }

        return image;
    }

    // Helper function to check if the move is within bounds and matches original color
    private boolean isValid(int[][] image, int row, int col, int originalColor) {
        int m = image.length, n = image[0].length;
        return row >= 0 && row < m &&
               col >= 0 && col < n &&
               image[row][col] == originalColor;
    }
}

```

---

## ✅ Time and Space Complexity

|Aspect|Complexity|
|---|---|
|**Time**|`O(m * n)` in worst case, where all pixels are filled|
|**Space**|`O(m * n)` for queue in worst case|
