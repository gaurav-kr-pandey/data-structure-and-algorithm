### [Practice - GFG](https://www.geeksforgeeks.org/problems/minimum-sum-partition3317/1)

Given an array **arr[]**  containing **non-negative** integers, the task is to divide it into two sets **set1** and **set2** such that the absolute difference between their sums is minimum and find the **minimum** difference.

**Examples:**

**Input**: `arr[] = [1, 6, 11, 5]`
**Output:** 1
**Explanation**: 
Subset1 = {1, 5, 6}, sum of Subset1 = 12 
Subset2 = {11}, sum of Subset2 = 11   
Hence, minimum difference is 1.  

## Intuition:

As stated in the problem, we need two subset s1 and s2 such that:

```java
| s1 - s2 | = minimum
```

Key observation:
	 As minimum as possible will be ZERO (0) because,  if both set are equal then difference will be zero

Hence, we can say that:
```java
2 * s1 == sum(arr), iff s1 == s2
target(s1) == sum(arr) / 2
```

now, we can also say that find the maximum subset sum closest to `target(s1) = sum(arr) / 2` or this problem is exactly as -

> Find the maximum subset sum is similar to picking the maximum value of items in knapsack in [[01 - Knapsack]]
>	 `w = sum(arr) / 2 == target`
>	 `value[] = = arr[]`
>	 `weight[]`, *not given (we just need to maximise the value)*

Hence, `Algorithm` to solve this problem is:
- Get `totalSum` of array
- `Target` will be `totalSum / 2`
- Get `maximumSubsetSum` for the `Target`
- result will be - 
```java
| totalSum - (2 * maximumSubsetSum(target = totalSum / 2)) |
```

**Code:**

```java
class Solution {

    public int minDifference(int arr[]) {
        int totalSum = Arrays.stream(arr).sum();
        int n = arr.length;
        int targetSum = totalSum / 2;
        Integer[][] dp = new Integer[n + 1][targetSum + 1];
        int max = maximumSubsetSum(arr, dp, n, targetSum);
        return Math.abs(totalSum - 2 * max);
    }
    
    
    // Code of Knapsack will give maximumSubsetSum
    private int maximumSubsetSum(int[] arr, Integer[][] dp, int n, int targetSum) {
        
        if (targetSum == 0) {
            return 0;
        }
        
        if (n == 0) {
            return 0;
        }
        
        if (dp[n][targetSum] != null) {
            return dp[n][targetSum];
        }
        
        if (targetSum >= arr[n - 1]) {
            dp[n][targetSum] = Math.max(arr[n - 1] + maximumSubsetSum(arr, dp, n - 1, targetSum - arr[n - 1]), maximumSubsetSum(arr, dp, n - 1, targetSum));
        } else {
            dp[n][targetSum] = maximumSubsetSum(arr, dp, n - 1, targetSum);
        }
        
        return dp[n][targetSum];
    }
}
```