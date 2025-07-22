https://leetcode.com/problems/merge-intervals/description/

```java
class Solution {
    public int[][] merge(int[][] intervals) {

        List<int[]> res = new ArrayList<>();
        Arrays.sort(intervals, (i1, i2) -> i1[0] - i2[0]);
        int[] curr = intervals[0];

        for (int[] interval : intervals) {
            if (curr[1] >= interval[0]) {
                curr[1] = Math.max(curr[1], interval[1]);
            } else {
                res.add(curr);
                curr = interval;
            }
        }

        res.add(curr);

        return res.toArray(new int[res.size()][]);
    }
}
```
