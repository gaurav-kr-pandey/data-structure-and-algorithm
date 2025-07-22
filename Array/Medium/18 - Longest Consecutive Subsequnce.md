https://leetcode.com/problems/longest-consecutive-sequence/description/


```java
class Solution {
    public int longestConsecutive(int[] nums) {
    
        Set<Integer> seen = Arrays.stream(nums).collect(Collectors.toSet());
        int length = 0;
        
        for(int n : nums) {
            if(!seen.contains(n - 1)) {
                int currLen = 0;
                while(seen.contains(n++)) currLen++;
                length = Math.max(currLen, length);
            }
        }

        return length;
    }
}
```