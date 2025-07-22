[practice](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        // nums = [0,0,1,1,1,2,2,3,3,4]
        int length = nums.length;
        int lastDupIndex = 0;
        
        for(int i = 0; i < nums.length; i++) {
            if(i == lastDupIndex || (nums[lastDupIndex] == nums[i])) 
                continue;
            
            nums[lastDupIndex+1] = nums[i];
            lastDupIndex++;
        }

        return lastDupIndex+1;
    }
}
```