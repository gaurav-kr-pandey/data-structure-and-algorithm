### [Subset Sum Problem](https://www.geeksforgeeks.org/problems/subset-sum-problem-1611555638/1)
Given an array of positive integers **arr[]** and a value **sum**, determine if there is a subset of **arr[]** with sum equal to given **sum**. 

**Examples:**

**Input**: arr[] = [3, 34, 4, 12, 5, 2], sum = 9  
**Output:** true 
**Explanation**: Here there exists a subset with target sum = 9, 4+3+2 = 9.

**Input**: arr[] = [3, 34, 4, 12, 5, 2], sum = 30
**Output:** false
**Explanation**: There is no subset with target sum 30.

**Input**: arr[] = [1, 2, 3], sum = 6
**Output:** true  
**Explanation**: The entire array can be taken as a subset, giving 1 + 2 + 3 = 6.

**Constraints:**  
1 <= arr.size() <= 200  
1<= arr[i] <= 200  
1<= sum <= 104

## Intution:

If we look carefully, this problem is similar to [[01 - Knapsack]], except it do not have value array.
Here `weight == sum` and we do not need to maximise the value, we just need to find if sum(weight) is possible or not with any subset in the array.


**Code:**

```java
class Solution {

    static Boolean isSubsetSum(int arr[], int sum) {
        int n = arr.length;
        Boolean[][] dp = new Boolean[sum + 1][n + 1];
        isSubsetSum(arr, dp, sum, n);
        return dp[sum][n];
    }
    
    static boolean isSubsetSum(int arr[], Boolean[][] dp, int sum, int n) {
        if (sum == 0) {
            return true;
        }
        
        if (n == 0) {
            return false;
        }
        
        if (dp[sum][n] != null) {
            return dp[sum][n];
        }
        
        if (sum >= arr[n - 1]) {
            dp[sum][n] = isSubsetSum(arr, dp, sum - arr[n - 1], n - 1) || isSubsetSum(arr, dp, sum, n - 1);
        } else {
            dp[sum][n] = isSubsetSum(arr, dp, sum, n - 1);
        }
        
        return dp[sum][n];
    }
}
```


