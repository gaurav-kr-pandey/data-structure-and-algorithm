### [Perfect Sum Problem](https://www.geeksforgeeks.org/problems/perfect-sum-problem5633/1)

Given an array **`arr`** of non-negative integers and an integer **`target`**, the task is to count all subsets of the array whose sum is equal to the given `target`.

**Examples:**

**Input**: arr[] = [5, 2, 3, 10, 6, 8], target = 10
**Output:** 3
**Explanation**: The subsets {5, 2, 3}, {2, 8}, and {10} sum up to the target 10.

**Input**: arr[] = [2, 5, 1, 4, 3], target = 10
**Output:** 3
**Explanation**: The subsets {2, 1, 4, 3}, {5, 1, 4}, and {2, 5, 3} sum up to the target 10.

**Input**: arr[] = [5, 7, 8], target = 3  
**Output:** 0
**Explanation**: There are no subsets of the array that sum up to the target 3.

**Input**: arr[] = [35, 2, 8, 22], target = 0  
**Output:** 1
**Explanation**: The empty subset is the only subset with a sum of 0.

**Constraints:**  
1 ≤ arr.size() ≤ 103  
0 ≤ arr[i] ≤ 103  
0 ≤ target ≤ 103

## Solution

This problem is variation of [[02 - Subset Sum Problem]]
In this problem we will count both choices:
1. Pick current element
2. Do not pick current element

```java

class Solution {
    
    int mod = 1000000007;
    
    public int perfectSum(int[] nums, int target) {
        int n = nums.length;
        int[][] dp = new int[n + 1][target + 1];
        
        for (int[] row : dp) {
            Arrays.fill(row, -1);
        }
        
        dp[n][target] = perfectSum(nums, dp, n, target) % mod;
        return dp[n][target] % mod;
    }
    
    public int perfectSum(int[] nums, int[][] dp, int n, int target) {

        if (n == 0) {
            if (target == 0) {
                return 1;
            }
            return 0;
        }
        
        
        if (dp[n][target] != -1) {
            return dp[n][target] % mod;
        }

		int notPick = perfectSum(nums, dp, n - 1, target) % mod;
        if (target >= nums[n - 1]) {
	        int pick = perfectSum(nums, dp, n - 1, target - nums[n - 1]) % mod;
            dp[n][target] = (pick + notPick) % mod;
        } else {
            dp[n][target] = notPick;
        }
        
        return dp[n][target] % mod;
    }
}

```

