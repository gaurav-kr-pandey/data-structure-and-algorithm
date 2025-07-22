https://leetcode.com/problems/pascals-triangle/description/

Given an integer `numRows`, return the first numRows of **Pascal's triangle**.
In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:
![[Pasted image 20250722215930.png]]

## Solution:

**Key Observation :**
- Each list has total value in increasing sequence (1, 2, 3, 4, 5), if input is 5 then there will be 5 rows
- Value of first(index 0) and last index(n) of each list is `1`
- If index is not `0` or `n - 1` then, `matrix[i][j] == matrix[i - 1][j - 1] + matrix[i - 1][j]`

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {

        List<List<Integer>> pascalTriangle = new ArrayList<>();

        for (int row = 0; row < numRows; row++) {
            List<Integer> curr = new ArrayList<>(row + 1);

            for (int col = 0; col < row + 1; col++) {
                if (col == 0 || col == row) {
                    curr.add(1);
                } else {
                    List<Integer> prevRow = pascalTriangle.get(row - 1);
                    curr.add(prevRow.get(col - 1) + prevRow.get(col));
                }
            }
            
            pascalTriangle.add(curr);
        }

        return pascalTriangle;
    }
}
```

