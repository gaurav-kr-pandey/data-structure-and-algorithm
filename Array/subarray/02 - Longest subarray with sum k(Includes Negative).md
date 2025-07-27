https://www.geeksforgeeks.org/problems/longest-sub-array-with-sum-k0809/1


### Solution:

This is exact same problem as - [[03 - Longest Subarray with 0 Sum (Includes Negative)]]

```java
class Solution {

    public int longestSubarray(int[] arr, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        int j = 0, n = arr.length, len = 0, sum = 0;

        while (j < n) {
            sum += arr[j];

            if (sum == k) {
                len = j + 1;
            }

            if (map.containsKey(sum - k)) {
                len = Math.max(len, j - map.get(sum - k));
            }

            map.putIfAbsent(sum, j);
            j++;
        }

        return len;
    }
}

```