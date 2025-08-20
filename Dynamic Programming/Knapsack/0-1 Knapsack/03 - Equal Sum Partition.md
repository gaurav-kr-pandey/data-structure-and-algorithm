### [Partition Equal Subset Sum](https://www.geeksforgeeks.org/problems/subset-sum-problem2014/1)

Given an array **arr[],** determine if it can be partitioned into two subsets such that the sum of elements in both parts is the **same.**

**Note:** Each element must be in exactly one subset.

**Examples:**

**Input:** arr = `[1, 5, 11, 5]`
**Output:** true
**Explanation:** The two parts are `[1, 5, 5]` and `[11]`.

**Input:** arr = `[1, 3, 5]`
**Output:** false
**Explanation:** This array can never be partitioned into two such parts.
### Intuition

As we need two subset s1, s2 i.e; 
```lisp
s1 == s2
s1 + s2 == sum(arr)
2 * s1 = sum(arr)
// this means,
target(s1) == sum / 2
```

This problem is exactly as previous problem - [[02 - Subset Sum Problem]]
we just need to check two cases -
- sum(arr) should not odd as we can not find have s1 == s2 with sum(arr) == odd
- We need find if (sum / 2) is present as subset in the given array using same code as - [[02 - Subset Sum Problem]]

**Code:**

```java
class Solution {
    static boolean equalPartition(int arr[]) {
        int sum = Arrays.stream(arr).sum();
        
        if (sum % 2 != 0) {
            return false;
        }
        
        int n = arr.length;
        Boolean[][] dp = new Boolean[(sum/2) + 1][n + 1];
    
        return equalPartition(arr, dp, sum/2, n);
    }
    
    static Boolean equalPartition(int arr[], Boolean[][] dp, int sum, int n) {
        if (sum == 0) {
            return true;
        }
        
        if (n == 0) {
            return false;
        }
        
        if (dp[sum][n] != null) {
            return dp[sum][n];
        }
        
        if (sum > 0) {
            dp[sum][n] = equalPartition(arr, dp, sum - arr[n - 1], n -1) 
                || equalPartition(arr, dp, sum, n -1);
        } else {
            dp[sum][n] = equalPartition(arr, dp, sum, n -1);
        }
        
        return dp[sum][n];
    }
    
}
```