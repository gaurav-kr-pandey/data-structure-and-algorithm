https://leetcode.com/problems/majority-element/description/

```java
class Solution {
    public int majorityElement(int[] nums) {

        int count = 1;
        int ele = nums[0];
        int length = nums.length;

        for (int i = 1; i < length; i++) {
            if (nums[i] == ele) {
                count++;
            } else {
                count--;
                if (count == 0) {
                    ele = nums[i];
                    count = 1;
                }
            }
        }

        count = 0;
        for (int i : nums) {
            if (i == ele)
                count++;
        }

        return count > nums.length / 2 ? ele : 0;
    }
}
```