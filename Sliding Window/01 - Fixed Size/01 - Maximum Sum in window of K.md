https://www.geeksforgeeks.org/problems/max-sum-subarray-of-size-k5313/1

### Solution:

**Key Observation:**
`Only Postive Elements`, `Will not work if there are negative elements`, `size k window` `maximum sum`

#### Intuition:

![[Pasted image 20250831211946.png]]


#### Code:

```java
class Solution {

    public int maximumSumSubarray(int[] arr, int k) {
        int sum = 0, max = Integer.MIN_VALUE, n = arr.length;
        int i = 0, j = 0;

        while (j < n) {
		    // No DS(Deque, Queue) Used to Remove Elements

		    // Add curr element to window
            sum += arr[j];

			// Calculate result if condition meets
            if (j - i + 1 == k) {
	            // Calculate result
                max = Math.max(max, sum);
                // Shrink window
                sum -= arr[i];
                i++;
            }
			
			// Expand window
            j++;
        }

        return max;
    }
}
```

#### Time Complexity : $O(n)$
#### Space Complexity: $O(1)$
