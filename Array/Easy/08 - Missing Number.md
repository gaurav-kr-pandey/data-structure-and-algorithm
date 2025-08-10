[practice](https://leetcode.com/problems/missing-number/description/)

Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return _the only number in the range that is missing from the array._

**Example 1:**
**Input:** nums = [3,0,1]
**Output:** 2
**Explanation:** `n = 3` since there are 3 numbers, so all numbers are in the range `[0,3]`. 2 is the missing number in the range since it does not appear in `nums`.

### Intuition:

The very brute force approach can be using `SET` and add all the array elements into the set, then we can check from 1 to n for absence of a number. But this approach requires extra space complexity of O($n$).

We can optimise this by avoiding taking extra space and find sum of all the elements in the array and subtracting it to the total sum of $n$ natural numbers.

How to find the sum of n natural numbers?

$S_n = \dfrac{n * (n + 1)} {2}$

if $\sum i \to n$, assume $S_a$ = $sum(array)$ then,

missing number = 
$x = S_n - Sa$ 

**Code:**

```java
class Solution {
    public int missingNumber(int[] nums) {

        int n = nums.length;
        int totalArraySum = 0;

        for(int x : nums) {
            totalArraySum += x;
        }
            
        int sum = n * (n + 1) / 2;
        return sum - totalArraySum;
    }
}
```