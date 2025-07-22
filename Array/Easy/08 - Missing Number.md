[practice](https://leetcode.com/problems/missing-number/description/)

```java
class Solution {
    public int missingNumber(int[] nums) {

        int n = nums.length;
        int totalSum = 0;

        for(int x : nums) {
            totalSum += x;
        }
            
        int sum = n * (n + 1) / 2;
        return sum - totalSum;
    }
}
```