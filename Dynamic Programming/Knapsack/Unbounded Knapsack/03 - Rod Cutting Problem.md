### [Rod Cutting](https://www.geeksforgeeks.org/problems/rod-cutting0840/1)

Given a rod of length **n** inches and an array `price[]`, where `price[i]` denotes the value of a piece of length **i**. Your task is to determine the **maximum** value obtainable by **cutting up** the rod and selling the **pieces**.
**Note:** n = size of price, and `price[]` is **1-indexed** array.

**Example:**

**Input:** `price[] = [1, 5, 8, 9, 10, 17, 17, 20]`
**Output:** `22`  
**Explanation:** The maximum obtainable value is 22 by cutting in two pieces of lengths 2 and 6, i.e., `5 + 17 = 22`.

### Intuition:

**Key Observations** :
1. No restrictions on cutting same length of rod and selling pieces to maximise profit
2. `price[]` array is similar to `value[]` array in [[02 - Unbounded Knapsack]] problem
3. We can cut the rod of length `n`, where `n = price.length`
	1. Instead of weight array we can construct length array from length `1 --> n`
	2. Or even to optimise this, we can have a variable i == n because anyway length array will have incremented values from 1 --> n
4. Similarly there is no maximum weight given, we can again keep rod length L == weight (w)

So, this problem is exactly same as [[02 - Unbounded Knapsack]] problem, here are the comparison details -

| Unbounded Knapsack   | Rod Cutting                        |
| -------------------- | ---------------------------------- |
| `value[] arr`        | `price[] arr`                      |
| `weight[] arr`       | `length[] arr`                     |
| `w` = maximum weight | `length = price.length` rod length |

**Code:**

```java
class Solution {
    public int cutRod(int[] price) {
        int n = price.length;
		// We can eleminate this array by just using a varible of length n
        int[] length = new int[n];
        int i = 1;
        while(i <= n) {
            length[i - 1] = i;
            i++;
        }
        
        Integer[][] dp = new Integer[n + 1][n + 1];
        
        return cutRod(price, length, dp, n, n);
    }
    
    public int cutRod(int[] price, int[] length, Integer[][] dp, int totalLength, int n) {
        if (n == 0) {
            return 0;
        }
        
        if (totalLength == 0) {
            return 0;
        }
        
        if (dp[totalLength][n] != null) {
            return dp[totalLength][n];
        }
        
        int notPick = cutRod(price, length, dp, totalLength, n - 1);
        if (totalLength >= length[n - 1]) {
            int pick = price[n - 1] + cutRod(price, length, dp, totalLength - length[n - 1], n);
            dp[totalLength][n] = Math.max(pick, notPick);
        } else {
            dp[totalLength][n] = notPick;
        }
        
        return dp[totalLength][n];
        
    }
}
```