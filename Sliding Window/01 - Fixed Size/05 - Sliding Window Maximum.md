https://leetcode.com/problems/sliding-window-maximum/description/

You are given an array of integers `nums`, there is a sliding window of size `k` which is moving from the very left of the array to the very right. You can only see the `k` numbers in the window. Each time the sliding window moves right by one position.
Return _the max sliding window_.

**Example 1:**

**Input:** `nums` = `[1,3,-1,-3,5,3,6,7]`, k = 3
**Output:** `[3,3,5,5,6,7]`

**Explanation:** 

|         Window         | Max |
| :--------------------: | :-: |
| ==1 3 -1== -3 5 3 6 7  |  3  |
| 1 ==3 -1 -3== 5 3 6 7  |  3  |
| 1 3 ==-1 -3 5== 3 6 7  |  5  |
| 1 3 -1 ==-3 5 3== 6 7  |  5  |
| 1 3 -1 -3 ==5 3 6== 7  |  6  |
| 1 3 -1  -3 5 ==3 6 7== |  7  |

**Example 2:**
**Input:** `nums` = `[1]`, k = 1
**Output:** `[1]`

## Intuition:

TBD

## Code:

```java
class Solution {

    public int[] maxSlidingWindow(int[] nums, int k) {
    
        int n = nums.length, i = 0, j = 0, x = 0;
        int[] res = new int[n - k + 1];
        Deque<Integer> dq = new ArrayDeque<>();
        
        while (j < n) {
	       /** 
	        *   Remove elements which is out of current window == i -> j 
	        *   Elements before i is already scanned in previous window
	        */
            while (!dq.isEmpty() && dq.peekFirst() < i) {
                dq.removeFirst();
            }
	       /** 
	        *   Remove elements that is not maintaining the monotonic property 
	        *   Check if element at the last is less than curr
	        */
            while (!dq.isEmpty() && nums[dq.peekLast()] < nums[j]) {
                dq.removeLast();
            }
            // Add curr element in the Deque
            dq.add(j);
            // If window size == k, capture result
            if (j - i + 1 == k) {
                res[x++] = nums[dq.peek()];
                // Shift Left pointer
                i++;
            }
            // Shift right pointer
            j++;
        }
        return res;
    }
}
```