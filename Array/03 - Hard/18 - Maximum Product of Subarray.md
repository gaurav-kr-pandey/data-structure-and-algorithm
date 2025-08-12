https://leetcode.com/problems/maximum-product-subarray/

Given an integer array `nums`, find a subarray that has the largest product, and return _the product_.
The test cases are generated so that the answer will fit in a **32-bit** integer.

### Intuition:

**Approach 1:** 
Use two loops:
1st loop $i \to n$ --> Keeps track of starting point
2nd loop $j = (i + 1) \to n$ --> Keeps track of ending point
3rd loop $i \to j$ --> Product of all the elements from $i \to j$
_Time Complexity: O($n^3$)_

**Approach 2:** Two pointers ($i = 0, j = n -1$)




**Code:**


```java
class Solution {
    public int maxProduct(int[] nums) {

        int n = nums.length;
        int leftProd = 1;
        int rightProd = 1;
        int max = nums[0];

        for (int i = 0; i < n; i++) {

            int j = n - 1 - i;

            leftProd = leftProd == 0 ? 1 : leftProd;
            rightProd = rightProd == 0 ? 1 : rightProd;

            leftProd *= nums[i];
            rightProd *= nums[j];

            max = Math.max(max, Math.max(leftProd, rightProd));
        }

        return max;
    }
}
```
