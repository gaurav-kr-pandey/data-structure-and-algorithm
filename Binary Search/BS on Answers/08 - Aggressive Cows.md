You are given an array with unique elements of **stalls[]**, which denote the positions of **stalls**. You are also given an integer **k** which denotes the number of aggressive cows. The task is to assign **stalls** to **k** cows such that the **minimum distance** between any two of them is the **maximum** possible.

https://www.geeksforgeeks.org/problems/aggressive-cows/1

## Intuition:

**Observations:**
- `stalls[i]` _$\to$ positions of cows_
- `k`  $\to$ _number of aggressive cows_
- _assign **stalls** to **k** cows such that the **minimum distance** between any two of them is the **maximum** possible_
- unsorted array
- distance between two stalls is calculated by `stalls[j] - stalls[i]` , where j > i

**What is the minimum possible difference between two cows ?**
We know we can not place two cows at the same stall, hence only minimum possible difference can be `1` if two cows are placed in adjacent stalls.

**What is the maximum possible difference between two cows ?**
It depends on total numbers of stalls. We can find the total number of stalls by finding max(stalls). Let's assume $m$ be the total number of stalls. 
max difference between two cows $\neq m$, because it will be:

```pgsql
max difference = max(stalls) - (min = 1)
```

now, my answer lies in $min \to max$, because I need to maximise the minimum difference between two cows.

**Approach 1:**
start from $diff = min \to max$ and check if we can place all the `k` cows linearly such that difference between two cows:

```java
diff >= stalls[j] - stalls[i]
/**
	Here j > i, we are assuming two pointers running from j = 1, i = 0 --> n
	and checking if we can place k cows as stated above
*/
```

_If n = length of array, and m = max value of array _
- _Time Complexity:_ $O(n * m)$ 
- _Space Complexity:_ $O(1)$

**Approach 2:**
If we look closely we have a $min = 1$ and a $max  = max(array)$, that can be a answer space for a binary search algorithm and we can reduce the time complexity of linearly traversing from $(min = 1) \to max$  to logarithmic($log_2 m$) time complexity.
_If n = length of array, and m = max value of array _
- _Time Complexity:_ $O(n log n) + O(n log m)$ 
	- _sorting = n log (n) + (diff  = log (m) x traversing n elements log m times) _
- _Space Complexity:_ $O(1)$


```text
Rough Algo:
- Sort the array
- high = max(array)
- low = minimum diff possible = 1
- everytime we calculate mid = diff 
- if diff can be place all k cows
	- low = mid + 1 // try for larger diff
	- update max
- else 
	- high = mid - 1 // try for smaller diff
```




**Code:**

```java
class Solution {

    public int aggressiveCows(int[] stalls, int k) {
        Arrays.sort(stalls);
        int n = stalls.length;
        int low = 1, high = stalls[n - 1] - stalls[0];
        int max = 1;
        
        while (low <= high) {
            int mid = (low + high)/2;
            
            if (canPlace(stalls, k, mid)) {
                low = mid + 1;
                max  = mid;
            } else {
                high = mid - 1;
            }
        }
        
        return max;
    }
    
    private boolean canPlace(int[] stalls, int k, int dist) {
        int n = stalls.length, cows = 1;
        int i = 0, j = 1;
        
        while (j < n && cows != k) {
            if (stalls[j] - stalls[i] >= dist) {
                cows++;
                i = j;
            }
            j++;
        }
        
        return k == cows;
    }
}
```