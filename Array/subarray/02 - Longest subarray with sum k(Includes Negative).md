https://www.geeksforgeeks.org/problems/longest-sub-array-with-sum-k0809/1

This is exact same problem as - [[03 - Longest Subarray with 0 Sum (Includes Negative)]]
### Intuition:

You might start thinking of using sliding window approach ([[11 - Longest Subarray with given Sum K(Positives)]]) and it works perfectly well for array with only positive numbers but will not work, if array has negative number, let's understand this with an example:
**Input:** arr[] = [10, 5, 2, 7, 1, -10], k = 15
**Output:** 6 (0 ---> 5)

If we consider above example to run a simple sliding window, we keep adding `currSum += arr[i]` till we reach `k = 15`

`if currSum <= 15 (k)` --> add current element `currSum += arr[i]`  
`if currSum == 15 (k)` --> calculate result`
`if currSum > 15 (k) -->` subtract element out of window range `currSum -= arr[j++]` 

Let's run this algo on above input -

|  i  |  j  | currSum | max(length = `i - j + 1`) |
| :-: | :-: | :-----: | :-----------------------: |
|  0  |  0  |   10    |             0             |
|  1  |  0  |  `15`   |       1 - 0 + 1 = 2       |
|  2  |  0  |   17    |                           |
|  2  |  1  |    7    |                           |
|  3  |  1  |   14    |                           |
|  4  |  1  |  `15`   |       4 - 1 + 1 = 4       |
|  5  |  1  |    5    |                           |
|     |     |         |     `max (4, 2) = 4`      |

Here answer from Sliding window is `4` but it should have been 6 since sum of complete array is 15, which has length 6, it is max length that is expected in the question. Now the question is:

###### Why Sliding Window does not worked for array having negative elements?

In sliding window we keep increasing the window and decreasing the window based on the variable and when `currSum > k` in that case we ~~==decrease the window==~~
_**Decreasing the window if  `currSum > k` is the issue**_ : because we are assuming that going ahead this sum will always increase but there can be a negative number that can reduce our `currSum` value and later sum up to `currSum == k` i.e; 
`currSum > k --> currSum <= k --> currSum == k` and we can have a bigger length array possibly. Hence, we are not checking for all the window that can have `currSum == k` and then finding max.

One approach could be having two loop just to find all possible window and another loop for adding that window's elements but time complexity will be O($n^3$), we can reduce this approach to O($n^2$) by precomputing sum into a prefix sum array but that is still not an optimal solution.

Let's figure out another approach that runs in O($n$) time complexity and if required may be O($n$) space complexity, we will use same input array:

**Input:** arr[] = [10, 5, 2, 7, 1, -10], k = 15

Let's build all the possible window that has `sum == k` **without decreasing variable window size = k** and try to find our solution:

|  i  |    currSum     | max(length = `i - j + 1`) |
| :-: | :------------: | :-----------------------: |
|  0  |       10       |             0             |
|  1  | 10 + 5 = `15`  |       1 - 0 + 1 = 2       |
|  2  |  15 + 2 = 17   |                           |
|  3  |  17 + 7 = 24   |                           |
|  4  |  24 + 1 = 25   |                           |
|  5  | 25 - 10 = `15` |       5 - 1 + 1 = 4       |
In this approach we are not decreasing the window and hence we kind of builded a `prefixSumMap <currSum, currIndex)>` and we got two values where `currSum == k`, hence

```text
0 --> 1 == 15
0 --> 5 == 15
```

we can get these values easily by adding extra check:
```java 
if (currSum == k) {
	maxLength = i + 1;
}
```

One more thing to notice is we are missing values that are not starting from `index = 0`, meaning values between `i >=0 && i < n`, for example

```text
sum of index (1, 2, 3, 4) ==> 15
```

To handle this, you might have observed that value of currSum at index 4 = 25
So, if there is a sum that is equals to 15 ending at index 4 from other previous index then there must be a sum, index in the prefixSumMap that is equals currSum - k because:

```text
sum[i --> j] + currSum == k then, 
sum[i --> j] == currSum - k
```

hence, we just need to check at each element that if there exists a element in the map that has value currSum - k, the we have a sum[i --> j] that can sum into currSum and is equals k.

Note: We can put the values only if it does not exists otherwise our currSum value will override the leftMost index that can give use the longest length;

Here is the complete soltion that works well:

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

---

| Array Type                | Approach              | Time Complexity | Space Complexity |
| ------------------------- | --------------------- | --------------- | ---------------- |
| **Only Positive Numbers** | Sliding Window        | O(n)            | O(1)             |
| **May Contain Negatives** | Prefix Sum + Hash Map | O(n)            | O(n)             |

