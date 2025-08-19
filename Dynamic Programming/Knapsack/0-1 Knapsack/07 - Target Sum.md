### [Target Sum](https://www.geeksforgeeks.org/problems/target-sum-1626326450/1)

Given an array of integers `A[]` of length `N` and an integer **target**.  
You want to build an **expression** out of **A** by adding one of the symbols '**+**' and '**-**' before each integer in **A** and then concatenate all the integers.
- For example, if `arr = {2, 1}`, you can add a '**+**' before 2 and a '**-**' before 1 and concatenate them to build the expression "+2-1".
Return the number of different **expressions** that can be built, which evaluates to **target** and return your answer with **modulo $10^9 + 7$**.

**Example 1:**
**Input:**
N = 5
A[] = {1, 1, 1, 1, 1}
target = 3
**Output:** 5
**Explanation:**
There are 5 ways to assign symbols to make the sum of `nums` be target 3.
```java
-1 + 1 + 1 + 1 + 1 = 3
+1 - 1 + 1 + 1 + 1 = 3
+1 + 1 - 1 + 1 + 1 = 3
+1 + 1 + 1 - 1 + 1 = 3
+1 + 1 + 1 + 1 - 1 = 3
```

**Your Task:**  
The task is to complete the function **findTargetSumWays**() which finds and returns the number of different expressions that can be built with modulo 109 + 7.

**Expected Time Complexity:** $O(n * sum)$, where sum refers to the range of sum possible.  
**Expected Auxiliary Space:** $O(n)$.
## Solution

If we think this way -
There will be few subset s1 which will be assigned '+' and few subset s2 with '-'
Then, 
```java
| s1 - s2 | = target --> equation1
// target is given as input
```

similarly, 
```java
s1 + s2 = sum(arr) --> equation2
```

From Equation 1 and 2, we can derive:
```java
(s1 - s2) + (s1 + s2) = (target + sum)
2 x s1 = target + sum
s1 = (target + sum) / 2
```

Now, we just need to find the count the subsets of `s1 == target ` as this problem [[04 - Count of Subset Sum]]

This problem is combination previous two problem - [[06 - Count number of subset with given difference]] and [[04 - Count of Subset Sum]]

**Code:**

```java

class Solution {
    static int findTargetSumWays(int n, int[] arr, int target) {
        int totalSum = Arrays.stream(arr).sum();
        
        if ((totalSum + target) % 2 != 0 || Math.abs(target) > totalSum) {
            return 0;
        }
        
        int sum = (target + totalSum) / 2;
        Integer[][] dp = new Integer[n + 1][sum + 1];
        dp[n][sum] = countSum(arr, dp, sum, n);
        return dp[n][sum];
    }
    
    static int countSum(int[] arr, Integer[][] dp, int target, int n) {
        if (n == 0) {
        // current and this [[04 - Count of Subset Sum]] problem need to be executed till end of the array since we need all the target even with zero, ex - arr = [0, 0, 0] , because we need count here
            if (target == 0) {
                return 1;
            }
            return 0;
        }
        
        if (dp[n][target] != null) {
            return dp[n][target];
        }
        
        if (target >= arr[n - 1]) {
            dp[n][target] = countSum(arr, dp, target - arr[n - 1], n -1) + countSum(arr, dp, target, n -1);
        } else {
            dp[n][target] = countSum(arr, dp, target, n -1);
        }
        
        return dp[n][target];
    }
}

```

