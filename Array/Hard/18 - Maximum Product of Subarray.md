https://leetcode.com/problems/maximum-product-subarray/

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
