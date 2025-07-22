https://leetcode.com/problems/pascals-triangle/description/

```java
class Solution {
    public List<List<Integer>> generate(int numRows) {

        List<List<Integer>> pT = new ArrayList<>();

        for (int row = 0; row < numRows; row++) {
            List<Integer> curr = new ArrayList<>(row + 1);

            for (int col = 0; col < row + 1; col++) {
                if (col == 0 || col == row) {
                    curr.add(1);
                } else {
                    List<Integer> prevRow = pT.get(row - 1);
                    curr.add(prevRow.get(col - 1) + prevRow.get(col));
                }
            }
            
            pT.add(curr);
        }

        return pT;
    }
}
```

