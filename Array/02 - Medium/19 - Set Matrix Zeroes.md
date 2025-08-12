https://leetcode.com/problems/set-matrix-zeroes/description/

```java
class Solution {
    public void setZeroes(int[][] matrix) {
        boolean hasFirstColZero = false;
        boolean hasFirstRowZero = false;

        int n = matrix.length, m = matrix[0].length;

        for (int i = 0; i < n; i++) {
            for(int j = 0; j < m; j++) {
                if (matrix[i][j] == 0) {
                    if (i == 0) hasFirstRowZero = true;
                    if (j == 0) hasFirstColZero = true;

                    matrix[0][j] = 0;
                    matrix[i][0] = 0;

                }
            }
        }

        for (int i = 1; i < n; i++) {
            for(int j = 1; j < m; j++) {
                if (matrix[0][j] == 0 || matrix[i][0] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        if (hasFirstRowZero) {
            Arrays.fill(matrix[0], 0);
        }

        if (hasFirstColZero) {
            for (int i = 0; i < n; i++) {
                matrix[i][0] = 0;
            }
        }

    }
}
```