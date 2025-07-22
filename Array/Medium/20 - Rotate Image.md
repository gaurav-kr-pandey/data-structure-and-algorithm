https://leetcode.com/problems/rotate-image/description/

```java
class Solution {
    public void rotate(int[][] matrix) {

        int row = matrix.length;
        int col = matrix[0].length;

        for(int i=0; i<row; i++) {
            for(int j=0; j<i; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        for(int i=0; i<row; i++) {
            reverse(matrix[i]);
        }
    }

    private void swap(int[] row, int i, int j) {
        int temp = row[i];
        row[i] = row[j];
        row[j] = temp;
    }

    private void reverse(int[] row) {
        int i=0; int j=row.length-1;
        while(i<j) {
            swap(row, i, j);
            i++;
            j--;
        }
    }
}
```