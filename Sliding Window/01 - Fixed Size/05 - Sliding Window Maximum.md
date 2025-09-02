https://leetcode.com/problems/sliding-window-maximum/description/

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.
Return _the max sliding window_.

**Example 1:**

**Input:** `nums` = `[1,3,-1,-3,5,3,6,7]`, k = 3
**Output:** `[3,3,5,5,6,7]`
**Explanation:** 
`Window position`                `Max`
---------------               -----
`[1  3  -1]` -3  5  3  6  7       **3**
 1 `[3  -1  -3]` 5  3  6  7       **3**
 1  3 `[-1  -3  5]` 3  6  7      **5**
 1  3  -1 `[-3  5  3]` 6  7       **5**
 1  3  -1  -3 `[5  3  6]` 7       **6**
 1  3  -1  -3  5 `[3  6  7]`      **7**

**Example 2:**

**Input:** `nums` = `[1]`, k = 1
**Output:** `[1]`




## Code:

```java
class Solution {

    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length, i = 0, j = 0, x = 0;
        int[] res = new int[n - k + 1];
        Deque<Integer> dq = new ArrayDeque<>();
        while (j < n) {
            while (!dq.isEmpty() && dq.peekFirst() < i) {
                dq.removeFirst();
            }
            while (!dq.isEmpty() && nums[dq.peekLast()] < nums[j]) {
                dq.removeLast();
            }
            dq.add(j);
            if (j - i + 1 == k) {
                res[x++] = nums[dq.peek()];
                i++;
            }
            j++;
        }
        return res;
    }
}
```