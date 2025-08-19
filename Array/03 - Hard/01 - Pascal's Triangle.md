https://leetcode.com/problems/pascals-triangle/description/

Given an integer `numRows`, return the first numRows of **Pascal's triangle**.
In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:

## Solution:

**Key Observation :**
- Each list has total value in increasing sequence (1, 2, 3, 4, 5), if input is 5 then there will be 5 rows ![[Pasted image 20250819102535.png]]
- Value of first(index 0) and last index(n) of each list is `1`
  ![[Pasted image 20250819103320.png]]
- If index is not `0` or `n - 1` then, `matrix[i][j] == matrix[i - 1][j - 1] + matrix[i - 1][j]` ![[Pasted image 20250819104118.png]]

**Code:**

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

