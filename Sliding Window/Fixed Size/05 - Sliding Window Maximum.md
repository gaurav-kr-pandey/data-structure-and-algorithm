
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