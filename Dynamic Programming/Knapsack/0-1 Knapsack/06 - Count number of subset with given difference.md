### [Partitions with Given Difference](https://www.geeksforgeeks.org/problems/partitions-with-given-difference/1)

Given an array **arr[]**, partition it into two subsets(possibly empty) such that each element must belong to only one subset. Let the sum of the elements of these two subsets be **sum1** and **sum2**. Given a difference **d**, count the number of partitions in which **sum1** is greater than or equal to **sum2** and the difference between **sum1** and **sum2** is equal to **d**. 

**Examples :**

**Input:** arr[] =  [5, 2, 6, 4], d = 3
**Output:** 1
**Explanation:** There is only one possible partition of this array. Partition : {6, 4}, {5, 2}. The subset difference between subset sum is: (6 + 4) - (5 + 2) = 3.

**Input:** arr[] = [1, 1, 1, 1], d = 0   
**Output:** 6   
**Explanation:** We can choose two 1's from indices {0,1}, {0,2}, {0,3}, {1,2}, {1,3}, {2,3} and put them in sum1 and remaning two 1's in sum2.  
Thus there are total 6 ways for partition the array arr. 

**Input:** arr[] = [1, 2, 1, 0, 1, 3, 3], d = 11  
**Output:** 2

**Constraint:**  
1 <= arr.size() <= 50  
0 <= d  <= 50  
0 <= arr[i] <= 6

## Solution

As given in problem statement that, we need to subsets s1 and s2 such that
	 | s1 - s2 | = d --> 1
	where d is given as input
Now, we know that
	 s1 + s2 = sum(arr) --> 2
If we solve above two equation
	`(s1 - s2) + (s1 + s2) = d + sum`
	 `2 * s1 = d + sum`
	 `s1 = (d + sum) / 2`
	 if we count s1 as `target` value like we have done in [[04 - Count of Subset Sum]]
	we will get our total count of subset == d.
so this problem is variation of [[04 - Count of Subset Sum]] problem.
	Edge case - check 
	`if ((sum + d) % 2 != 0 || sum < d) return 0;`

Here is the algo:
1. Initialise `sum` = sum(arr);
2. handle edge case as discussed above
3. calculate `target = (sum + d) / 2`, d is given in the input
4. count of subset sum == target


```java
class Solution {
    int countPartitions(int[] arr, int diff) {
        int n =arr.length;
        
        int sum = Arrays.stream(arr).sum();
        
        if ((sum + diff) % 2 != 0 || sum < diff) return 0;

        int target = (sum + diff) / 2;
        Integer[][] dp = new Integer[n + 1][target + 1];
        count(arr, dp, target, n);
        return dp[n][target];
    }
    
    int count(int[] arr, Integer[][] dp, int target, int n) {
        
        if (n == 0) {
            if (target == 0) {
                return 1;
            }
            return 0;
        }
        
        if (dp[n][target] != null) {
            return dp[n][target];
        }
        
        if (arr[n - 1] <= target) {
            dp[n][target] = count(arr, dp, target - arr[n - 1], n -1)
                                + count(arr, dp, target, n -1);
        } else {
            dp[n][target] = count(arr, dp, target, n -1);
        }
        
        return dp[n][target];
    }
}

```