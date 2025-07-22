### [Practice - GFG](https://www.geeksforgeeks.org/problems/0-1-knapsack-problem0945/1)

Given **n** items, each with a specific **weight** and **value**, and a knapsack with a capacity of **W**, the task is to put the items in the knapsack such that the **sum of weights of the items <= W** and the **sum of values** associated with them is **maximised**. 

**Note:** You can either place an item entirely in the bag or leave it out entirely. Also, each item is available in **single** quantity.

**Examples :**

**Input:** W = 4, `val[]` = [1, 2, 3], `wt[]` = [4, 5, 1]   
**Output:** 3  
**Explanation:** Choose the last item, which weighs 1 unit and has a value of 3.

**Input:** W = 3, `val[]` = [1, 2, 3], `wt[]` = [4, 5, 6]   
**Output:** 0  
**Explanation:** Every item has a weight exceeding the knapsack's capacity (3).

**Input:** W = 5, `val[]` = [10, 40, 30, 50], `wt[]` = [5, 4, 2, 3]   
**Output:** 80  
**Explanation:** Choose the third item (value 30, weight 2) and the last item (value 50, weight 3) for a total value of 80.

**Constraints:**  
2 ≤ val.size() = wt.size() ≤ 103  
1 ≤ W ≤ 103  
1 ≤ val[i] ≤ 103  
1 ≤ wt[i] ≤ 103



```java
class Solution {
    public int knapsack(int w, int val[], int wt[]) {
        int n = wt.length;
        Integer[][] dp = new Integer[n + 1][w + 1];
        return knapsack(w, n, val, wt, dp);
    }
    
    private int knapsack(int w, int n, int[] val, int[] wt, Integer[][] dp) {
    
        if (w == 0 || n == 0) {
            return 0;
        }
        
        if (dp[n][w] != null) {
            return dp[n][w];
        }
        
        if (w >= wt[n -1]) {
            int pick = val[n - 1] + knapsack(w - wt[n - 1], n - 1, val, wt, dp);
            int notPick = knapsack(w, n - 1, val, wt, dp);
            dp[n][w] = Math.max(pick, notPick);
        } else {
            int notPick = knapsack(w, n - 1, val, wt, dp);
            dp[n][w] = notPick;
        }
        
        return dp[n][w];
    }
}
```