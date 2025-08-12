https://leetcode.com/problems/merge-intervals/description/

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

**Example 1:**

**Input:** intervals = [[1,3],[2,6],[8,10],[15,18]]
**Output:** [[1,6],[8,10],[15,18]]
**Explanation:** Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

## Solution:

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
