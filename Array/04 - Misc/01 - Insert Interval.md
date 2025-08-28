### Problem
- Input:
    - `intervals` → sorted, non-overlapping intervals.
    - `newInterval` → single interval to insert.
- Task: Insert `newInterval` and merge overlapping intervals.

---
### Key Idea

Break it into **three phases**:
1. Add all intervals that come **before** `newInterval`.
2. Merge all intervals that **overlap** with `newInterval`.
3. Add all intervals that come **after** `newInterval`.

---
### Algorithm

1. Initialize result list.
2. Traverse intervals:
    - If `intervals[i][1] < newInterval[0]` → add interval (before case).
    - If `intervals[i][0] <= newInterval[1]` → overlap → merge by updating:
        `newInterval[0] = min(newInterval[0], intervals[i][0])`
        `newInterval[1] = max(newInterval[1], intervals[i][1])`
    - Otherwise → interval is after → break loop.
3. Add merged `newInterval`.
4. Add the rest of the intervals.

---
### Complexity

- **Time**: O(n) (single pass).
- **Space**: O(n) (for result list).

### Code:

```java
class Solution {
    public int[][] insert(int[][] intervals, int[] curr) {
        List<int[]> result = new ArrayList<>();
        int i = 0, n = intervals.length;

        // Step 1: add all intervals ending before curr starts
        while (i < n && intervals[i][1] < curr[0]) {
            result.add(intervals[i]);
            i++;
        }

        // Step 2: merge overlaps
        while (i < n && intervals[i][0] <= curr[1]) {
            curr[0] = Math.min(curr[0], intervals[i][0]);
            curr[1] = Math.max(curr[1], intervals[i][1]);
            i++;
        }
        result.add(curr);

        // Step 3: add remaining intervals
        while (i < n) {
            result.add(intervals[i]);
            i++;
        }

        return result.toArray(new int[result.size()][]);
    }
}
```