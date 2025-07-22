https://leetcode.com/problems/two-sum/description/

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {

        Map<Integer, Integer> seen = new HashMap<>();
        int len = nums.length;

        for (int i = 0; i < len; i++) {
            int x = target - nums[i];
            if (seen.containsKey(x)) {
                return new int[] {i, seen.get(x)};
            }
            seen.put(nums[i], i);
        }

        return new int[] {-1, -1};
    }
}
```