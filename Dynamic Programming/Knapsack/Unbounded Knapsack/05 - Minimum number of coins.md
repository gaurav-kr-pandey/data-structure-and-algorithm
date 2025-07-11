### [Coin Change (Minimum Coins)](https://www.geeksforgeeks.org/problems/number-of-coins1824/1)

You are given an array **coins[]**, where each element represents a coin of a **different** denomination, and a target value **sum**. You have an **unlimited** supply of each coin type {coins1, coins2, ..., coins m}.

Your task is to determine the **minimum** number of coins needed to obtain the target **sum**. If it is not possible to form the sum using the given coins, return **-1**.

**Examples:**

**Input:** coins[] = [25, 10, 5], sum = 30  
**Output:** 2  
**Explanation:** Minimum 2 coins needed, 25 and 5  

**Input:** coins[] = [9, 6, 5, 1], sum = 19  
**Output:** 3  
**Explanation:** 19 = 9 + 9 + 1

**Input:** coins[] = [5, 1], sum = 0  
**Output:** 0  
**Explanation:** For 0 sum, we do not need a coin

**Input:** coins[] = [4, 6, 2], sum = 5  
**Output:** -1  
**Explanation:** Not possible to make the given sum.

**Constraints:**  
1 ≤ sum * coins.size() ≤ 106
0 <= sum <= 104
1 <= coins[i] <= 104
1 <= coins.size() <= 103

## Solution

As stated in the question that we need to find the minimum number of coins that sums upto given sum in the question. We can use [[04 - Coin Change]]'s approach with slight variation where we will keep track of count at each steps.


```java

class Solution {

    public int minCoins(int coins[], int sum) {
        int n = coins.length;
        Integer[][] dp = new Integer[n + 1][sum + 1];
        int ans = minCoins(coins, dp, n, sum);
        return ans >= (int) 1e9 ? -1 : ans;
    }
    
    public int minCoins(int[] coins, Integer[][] dp, int n, int sum) {
        if (n == 0) {
            return 0;
        }
        
        if (sum == 0) {
            return 0;
        }
        
        if (dp[n][sum] != null) {
            return dp[n][sum];
        }
        
        int notPick = minCoins(coins, dp, n - 1, sum);
        notPick = notPick == 0 ? (int) 1e9 : notPick; // 1e9: Same as 10^9
        // We can use Integer.MAX_VALUE but adding +1 will lead to overflow into negative values
        
        if (sum >= coins[n - 1]) {
            int pick = 1 + minCoins(coins, dp, n, sum - coins[n - 1]);
            dp[n][sum] = Math.min(pick, notPick);
        } else {
            dp[n][sum] = notPick;
        }
        
        return dp[n][sum];
    }
}

```

