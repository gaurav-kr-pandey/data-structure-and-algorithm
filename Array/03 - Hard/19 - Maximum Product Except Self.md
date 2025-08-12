
https://leetcode.com/problems/product-of-array-except-self/description/


```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        // Computes postfix product from n - 1 --> 0
        int[] prod = new int[n];
        int[] res = new int[n];
        // Initialise
        prod[n - 1] = nums[n - 1];

        for (int i = n - 2; i >= 0; i--) {
            prod[i] = nums[i] * prod[i + 1];
        }

        res[0] = prod[1];
        
        int leftProd = nums[0];
        for (int i = 1; i < n - 1; i++) {
            res[i] = leftProd * prod[i + 1];
            leftProd *= nums[i];
        }

        res[n - 1] = leftProd;

        return res;
    }
}
```


**Optimal Version (Without Extra Space):**

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] res = new int[n];

        // Step 1: Compute prefix product
        res[0] = 1;
        for (int i = 1; i < n; i++) {
            res[i] = res[i - 1] * nums[i - 1];
        }

        // Step 2: Multiply with suffix product on the fly
        int rightProd = 1;
        for (int i = n - 1; i >= 0; i--) {
            res[i] = res[i] * rightProd;
            rightProd *= nums[i];
        }

        return res;
    }
}

```