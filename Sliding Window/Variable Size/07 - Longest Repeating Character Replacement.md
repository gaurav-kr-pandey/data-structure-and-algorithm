https://leetcode.com/problems/longest-repeating-character-replacement/description/

You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return _the length of the longest substring containing the same letter you can get after performing the above operations_.

**Example 1:**

**Input:** s = "ABAB", k = 2
**Output:** 4
**Explanation:** Replace the two 'A's with two 'B's or vice versa.
### Solution:

## Key Observations

- We can use the **sliding window** technique.
- In any window, to make all characters the same:
    - We **keep track of the count of the most frequent character** in the current window.
    - If total characters in window - most frequent character count > `k`, we **shrink** the window.
- We don’t need to track which character is majority — just **track the count of the max occurring character** in the current window.

```text
longest substring containing same letter(l) = letter with max freq(max_freq) + k
l = max_freq + k
```

---

## Intuition

In a window `[i...j]`, suppose:
- `windowSize = j - i + 1`
- `maxFreq = count of most frequent character in window`

Then:
```pgsql
if (windowSize - maxFreq) <= k
    -> window is valid
else
    -> shrink the window from left
```

##### Code :

```java
class Solution {

    public int characterReplacement(String s, int k) {
        
        int i = 0, j = 0, n = s.length(), maxFreq = 0, max = 0;
        int[] freq = new int[26];
        while (j < n) {
            freq[s.charAt(j) - 'A']++;
            maxFreq = Math.max(maxFreq, freq[s.charAt(j) - 'A']);
            while (j - i + 1 > k + maxFreq) {
                freq[s.charAt(i) - 'A']--;
                i++;
            }
            max = Math.max(max, j - i + 1);
            j++;
        }
        return max;
    }
}

```