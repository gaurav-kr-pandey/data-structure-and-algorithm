https://leetcode.com/problems/maximum-subarray/description/

Given an integer array `nums`, find the [[subarray]] with the largest sum, and return _its sum_.
**Example 1:**
**Input:** nums = `[-2,1,-3,4,-1,2,1,-5,4]`
**Output:** 6
**Explanation:** The subarray `[4,-1,2,1]` has the largest sum 6.

### Intuition:

**Approach 1:** $O(n^3)$ *Solution*
We will use three loops,
1st loop to keep track of starting point $i \to n$
2nd loop to keep track of ending at point $j = i + 1 \to n$
3rd loop to find $\sum i \to j$
then, we can maintain a max variable to keep track of largest sum

**Approach 2:** $O(n^2)$ _Time Complexity_ and, $O(n)$ _Space Complexity_
We will not use third loop, instead maintain a prefixSum array
create a prefixSum array
1st loop to keep track of starting point $i \to n$
2nd loop to keep track of ending at point $j = (i + 1) \to n$
find $\sum i \to j$,  using prefixSum array `currSum = prefixSum[j] - prefixSum[i] + arr[i]`
then, we can maintain a max variable to keep track of largest sum
Example:
arr = `[1, 2, 3, 4, 5, 6]`
prefixSum = `[1, 3, 6, 10, 15, 21]` 
currSum (i = 2, j = 5) = `prefixSum[5] - prefixSum[2] + arr[2]` = 18 (3 + 4 + 5 + 6)

**Approach 3:** $O(n)$ _Time Complexity_ [[Kaden's Algorithm]]



```java
class Solution {
    public int maxSubArray(int[] nums) {
        int currSum=0; int maxSum=Integer.MIN_VALUE;

        for(int i=0; i<nums.length; i++) {
            if(currSum+nums[i]>=nums[i]) {
                currSum+=nums[i];
            } else {
                currSum = nums[i];
            }

            maxSum = Math.max(currSum, maxSum);
        }

        return maxSum;
    }
}
```