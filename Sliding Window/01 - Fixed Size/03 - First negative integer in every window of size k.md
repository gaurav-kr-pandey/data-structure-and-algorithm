https://www.geeksforgeeks.org/problems/first-negative-integer-in-every-window-of-size-k3345/1

Given an array **arr[]**  and a positive integer **k**, find the first negative integer for each and every window(contiguous subarray) of size **k.**

**Note:** If a window does not contain a negative integer, then return 0 for that window.

**Examples:**

**Input:** arr[] = [-8, 2, 3, -6, 10] , k = 2
**Output:** [-8, 0, -6, -6]
**Explanation:**
Window [-8, 2] First negative integer is -8.
Window [2, 3] No negative integers, output is 0.
Window [3, -6] First negative integer is -6.
Window [-6, 10] First negative integer is -6.

### Solution:



```java
class Solution {

    static List<Integer> firstNegInt(int arr[], int k) {
        List<Integer> list = new ArrayList<>();
        Queue<Integer> q = new LinkedList<>();
        int i = 0, j = 0, n = arr.length;

        while (j < n) {
            // If we are using extra DS, then clear out of range values
            /// If required we can clear useless values here as well
            if (!q.isEmpty() && q.peek() < i) {
                q.poll();
            }

            if (arr[j] < 0) {
                q.add(j);
            }

            if (j - i + 1 == k) {
                // Calculate result
                list.add(q.isEmpty() ? 0 : arr[q.peek()]);
                // Shift left pointer by 1
                i++;
            }
            // Shift right pointer by 1
            j++;
        }

        return list;
    }
}

```