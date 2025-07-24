https://www.geeksforgeeks.org/problems/max-sum-subarray-of-size-k5313/1

### Solution:

**Key Observation:**
`Only Postive Elements`, `Will not work if there are negative elements`, `size k window` `maximum sum`


```java
class Solution {
    public int maximumSumSubarray(int[] arr, int k) {
        int sum = 0, max = Integer.MIN_VALUE, n = arr.length;
        int i = 0, j = 0;
        
        while (j < n) {
            sum += arr[j];
            
            if (j - i + 1 == k) {
                max = Math.max(max, sum);
                sum -= arr[i];
                i++;
            }
            
            j++;
        }
        
        return max;
    }
}
```