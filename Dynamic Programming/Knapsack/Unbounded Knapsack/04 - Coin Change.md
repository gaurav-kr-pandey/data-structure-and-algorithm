
### [Coin Change (Count Ways)](https://www.geeksforgeeks.org/problems/coin-change2448/1)

Given an integer array `coins[ ]` representing different denominations of currency and an integer **sum**, find(count) the number of ways you can make `sum` by using different combinations from `coins[ ].`   
**Note:** Assume that you have an **infinite** supply of each type of coin. Therefore, you can use any coin as many times as you want.  
Answers are guaranteed to fit into a 32-bit integer. 

**Examples:**

**Input:** `coins[] = [1, 2, 3], sum = 4`
**Output:** 4
**Explanation**: `Four Possible ways are: [1, 1, 1, 1], [1, 1, 2], [2, 2], [1, 3]`.

### Intuition

This problem is variation of [[04 - Count of Subset Sum]] problem except it is unbounded knapsack
because it is given in the problem that - "**Assume that you have an *infinite* supply of each type of coin**"

**Code:**

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