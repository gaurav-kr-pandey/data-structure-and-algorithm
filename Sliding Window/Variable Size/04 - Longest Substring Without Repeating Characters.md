https://leetcode.com/problems/longest-substring-without-repeating-characters/description/

### Solution:

```java
class Solution {

    public int lengthOfLongestSubstring(String s) {
        Set<Character> seen = new HashSet<>();
        int i = 0, j = 0, n = s.length(), max = 0;
        while (j < n) {
            while (i < j && seen.contains(s.charAt(j))) {
                seen.remove(s.charAt(i));
                i++;
            }
            seen.add(s.charAt(j));
            max = Math.max(max, j - i + 1);
            j++;
        }
        return max;
    }
}

```