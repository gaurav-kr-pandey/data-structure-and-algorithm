> **Problem**: Find the **length of the largest subarray** with **sum = 0** in an integer array `arr[]`.

[practice](https://www.geeksforgeeks.org/problems/largest-subarray-with-0-sum/1)


**Examples:**

**Input:** arr[] = [15, -2, 2, -8, 1, 7, 10, 23]
**Output:** 5
**Explanation:** The longest subarray with sum equals to 0 is [-2, 2, -8, 1, 7].

**Input:** arr[] = [2, 10, 4]
**Output:** 0
**Explanation:** There is no subarray with a sum of 0.

**Input:** arr[] = [1, 0, -4, 3, 1, 0]
**Output:** 5
**Explanation:** The longest subarray with sum equals to 0 is [0, -4, 3, 1, 0]

**Constraints:**  
1 ≤ arr.size() ≤ 106  
−103 ≤ arr[i] ≤ 103

## Solution

> `subarray` , `sum`, `includes negative numbers`, `length of longest subarray`

```java

class Solution {
    int maxLength(int arr[]) {
    
        int n = arr.length, max = 0, sum = 0;    
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < n; i++) {
            
            sum += arr[i];
            if (sum == 0) {
                /** 
	                Since we want longest length that sums = 0
	                therefor if currSum == 0 then we can directly assign i + 1
		            because from 0 --> i currZero is longest
		        **/
                max = i + 1;
            }
            
            if (map.containsKey(sum)) {
	            /**
		            If currSum exists that means there is a already a sum
	                If key exist, do not put map(sum, i)
	                because we want max length and if we put the curr sum
	                left most index will be overrided
	            **/
	            max = Math.max(max, i - map.get(sum));
            } else {
                map.put(sum, i);
            }
        }
        
        return max;
    }
}

```