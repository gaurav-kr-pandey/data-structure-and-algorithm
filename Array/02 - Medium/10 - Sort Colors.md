https://leetcode.com/problems/sort-colors/description/

```java
class Solution {
    public void sortColors(int[] nums) {
        int len = nums.length;
        int low = 0, mid = 0, high = len - 1;

        while(mid <= high) {
            int ele = nums[mid];
            switch(ele) {
                case 0: swap(nums, low, mid);
                        low++;
                        mid++;
                        break;
                case 1: mid++;
                        break;
                case 2: swap(nums, mid, high);
                        high--;
                        break;
            }
        }
    }

    private void swap(int[] nums, int i, int j) {
        int t = nums[i];
        nums[i] = nums[j];
        nums[j] = t;
    }
}
```

