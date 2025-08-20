## [Knapsack with duplicate items](https://www.geeksforgeeks.org/problems/knapsack-with-duplicate-items4201/1)

Given a set of items, each with a weight and a value, represented by the array **wt** and **val** respectively. Also, a knapsack with a weight limit **capacity**.  
The task is to fill the knapsack in such a way that we can get the maximum profit. Return the maximum profit.  
**Note:** Each item can be taken any number of times.

**Examples:**
**Input:** `val = [1, 1], wt = [2, 1], capacity = 3`
**Output:** 3
**Explanation:** The optimal choice is to pick the 2nd element 3 times.

### Intuition

As described in the problem, we can pick any item as many times as we need and maximise the profit by adding corresponding value;

Choices:
1. Pick element (repeat if required)
2. Do not pick and move on

**Code:**


```java
class Solution {
    public int knapSack(int val[], int wt[], int capacity) {
        int n = val.length;
        Integer[][] dp = new Integer[n + 1][capacity + 1];
        knapsack(val, wt, dp, capacity, n);
        return dp[n][capacity];
    }
    
    public int knapsack(int val[], int wt[], Integer[][] dp, int capacity, int n) {
        if (n == 0) {
            return 0;
        }
        
        if (capacity == 0) {
            return 0;
        }
        
        if (dp[n][capacity] != null) {
            return dp[n][capacity];
        }
        
        int notPick = knapsack(val, wt, dp, capacity, n - 1);
        if (wt[n - 1] <= capacity) {
		    int pick = val[n - 1] + knapsack(val, wt, dp, capacity - wt[n - 1], n);
            dp[n][capacity] = Math.max(pick, notPick);
        } else {
            dp[n][capacity] = notPick;
        }
        
        return dp[n][capacity];
    }
}
```