https://www.geeksforgeeks.org/problems/longest-k-unique-characters-substring0853/1

You are given a string **s** consisting only lowercase alphabets and an integer **k**. Your task is to find the **length** of the **longest substring** that contains exactly **k** distinct characters.

**Note :** If no such substring exists, return **-1**. 

**Examples:**

**Input:** s = "aabacbebebe", k = 3
**Output:** 7
**Explanation**: The longest substring with exactly 3 distinct characters is "cbebebe", which includes 'c', 'b', and 'e'.

### Solution:

```java
class Solution {

    public int longestKSubstr(String s, int k) {
        Map<Character, Integer> freq = new HashMap<>();
        int i = 0, j = 0, n = s.length(), max = -1;

        while (j < n) {
            char curr = s.charAt(j);
            freq.put(curr, freq.getOrDefault(curr, 0) + 1);

            while (freq.size() > k && i < j) {
                char prev = s.charAt(i);
                freq.put(prev, freq.get(prev) - 1);
                if (freq.get(prev) == 0) {
                    freq.remove(prev);
                }
                i++;
            }

            if (freq.size() == k) {
                max = Math.max(max, j - i + 1);
            }

            j++;
        }

        return max;
    }
}

```