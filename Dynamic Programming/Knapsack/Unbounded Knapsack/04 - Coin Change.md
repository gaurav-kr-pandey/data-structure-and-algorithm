
### [Coin Change (Count Ways)](https://www.geeksforgeeks.org/problems/coin-change2448/1)

Given an integer array **coins[ ]** representing different denominations of currency and an integer **sum**, find the number of ways you can make **sum** by using different combinations from coins[ ].   
**Note:** Assume that you have an **infinite** supply of each type of coin. Therefore, you can use any coin as many times as you want.  
Answers are guaranteed to fit into a 32-bit integer. 

**Examples:**

**Input:** coins[] = [1, 2, 3], sum = 4
**Output:** 4
**Explanation**: Four Possible ways are: [1, 1, 1, 1], [1, 1, 2], [2, 2], [1, 3].

**Input**: coins[] = [2, 5, 3, 6], sum = 10
**Output:** 5
**Explanation**: Five Possible ways are: [2, 2, 2, 2, 2], [2, 2, 3, 3], [2, 2, 6], [2, 3, 5] and [5, 5].  

**Input**: coins[] = [5, 10], sum = 3
**Output:** 0  
**Explanation:** Since all coin denominations are greater than sum, no combination can make the target sum.

**Constraints:**  
1 <= sum <= 103  
1 <= coins[i] <= 104  
1 <= coins.size() <= 103

## Solution

This problem is variation of [[04 - Count of Subset Sum]] problem except it is unbounded knapsack
because it is given in the problem that - "**Assume that you have an *infinite* supply of each type of coin**"


```java

class Solution {
    public int count(int coins[], int sum) {
        int n = coins.length;
        Integer[][] dp = new Integer[n + 1][sum + 1];
        return count(coins, dp, n, sum);
    }
    
    public int count(int coins[], Integer[][] dp, int n, int sum) {
        
        if (n == 0) {
            return 0;
        }
        
        if (sum == 0) {
            return 1;
        }
        
        if (dp[n][sum] != null) {
            return dp[n][sum];
        }
        
        if (sum >= coins[n - 1]) {
            dp[n][sum] = count(coins, dp, n, sum - coins[n - 1]) + count(coins, dp, n - 1, sum);
        } else {
            dp[n][sum] = count(coins, dp, n - 1, sum);
        }
        
        return dp[n][sum];
    }
}

```