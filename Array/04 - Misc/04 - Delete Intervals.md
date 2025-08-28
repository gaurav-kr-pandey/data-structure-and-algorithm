https://leetcode.com/problems/non-overlapping-intervals/description/

Given an array of intervals `intervals` where `intervals[i] = [starti, endi]`, return _the minimum number of intervals you need to remove to make the rest of the intervals non-overlapping_.
**Note** that intervals which only touch at a point are **non-overlapping**. For example, `[1, 2]` and `[2, 3]` are non-overlapping.


### Intuition:


### Code:

```java
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        int n = intervals.length, count = 0;
        Arrays.sort(intervals, (a, b) -> a[1] - b[1]);
        int prevEnd = intervals[0][1];

        for (int i = 1; i < n; i++) {
            int[] curr = intervals[i];
            if (prevEnd > curr[0]) {
                count++;
            } else {
                prevEnd = curr[1];
            }
        }

        return count;
    }
}
```