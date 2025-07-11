[practice](https://www.geeksforgeeks.org/problems/count-subarray-with-given-xor/1)

Given an array of integers **arr[]** and a number **k**, count the number of subarrays having **XOR** of their elements as **k**.

**Examples:** 

**Input:** arr[] = [4, 2, 2, 6, 4], k = 6  
**Output:** 4  
**Explanation:** The subarrays having XOR of their elements as 6 are [4, 2], [4, 2, 2, 6, 4], [2, 2, 6], and [6]. Hence, the answer is 4.

## Solution

🔹 Trick:  
If `prefixXor[j] ^ prefixXor[i-1] = k`, then:

```
prefixXor[i-1] = prefixXor[j] ^ k
```

🔹 Code:

```java
class Solution {
    public long subarrayXor(int arr[], int k) {
        
        int xor = 0, count = 0, n = arr.length;
        
        // HashMap to store frequency of prefix XORs
        // Key: prefixXor value, Value: count of occurrences
        Map<Integer, Integer> map = new HashMap<>();
        
        // Important: XOR of 0 elements is 0.
        // This allows subarrays starting from index 0 to be counted.
        map.put(0, 1);
        
        for (int i = 0; i < n; i++) {
            
            // Compute prefix XOR up to current index
            // Property used: a ^ 0 = a
            xor = xor ^ arr[i];
            
            // Required prefix XOR for current subarray to have XOR = k
            // If: prefixXor[j] ^ prefixXor[i-1] == k
            // Then: prefixXor[i-1] == prefixXor[j] ^ k
            // Rearranged using XOR rule: a ^ b = c → a = b ^ c
            int req = xor ^ k;
            
            // If required prefix XOR was seen before, add its frequency to count
            if (map.containsKey(req)) {
                count += map.get(req);
            }
            
            // Store/update frequency of current prefix XOR
            // Ensures that future subarrays can use it
            map.put(xor, map.getOrDefault(xor, 0) + 1);
        }
        
        return count;
    }
}

```

#### XOR Properties used

|Line|Concept|Property Used|
|---|---|---|
|`xor ^= arr[i];`|Building running XOR|`a ^ 0 = a`, `a ^ a = 0`|
|`int req = xor ^ k;`|Deriving the required prefixXor|`a ^ b = c` → `a = b ^ c`|
|`map.getOrDefault(xor, 0)`|Track how many times prefixXor occurred|Hash frequency count|
|`map.put(0, 1);`|Handles subarrays starting from index 0|XOR of empty prefix = 0|

