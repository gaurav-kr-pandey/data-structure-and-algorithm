https://leetcode.com/problems/maximum-average-subarray-i/description/



```java
class Solution {

    public double findMaxAverage(int[] nums, int k) {
        int i = 0, j = 0, n = nums.length;
        double sum = new Double(0);
        double max = (double) Integer.MIN_VALUE;
        while (j < n) {
            sum += nums[j];
            if (j - i + 1 == k) {
                double avg = new Double(sum / (double) k);
                max = Math.max(avg, max);
                sum = sum - nums[i];
                i++;
            }
            j++;
        }
        return max;
    }
}

```