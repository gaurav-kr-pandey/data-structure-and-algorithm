### Longest Common Substring

You are given two strings **s1** and **s2**. Your task is to find the length of the **longest common substring** among the given strings.

**Examples:**

**Input:** s1 = "ABCDGH", s2 = "ACDGHR"
**Output:** 4
**Explanation**: The longest common substring is "CDGH" with a length of 4.

**Input**: s1 = "abc", s2 = "acb"
**Output:** 1
**Explanation**: The longest common substrings are "a", "b", "c" all having length 1.

**Input**: s1 = "YZ", s2 = "yz"
**Output:** 0

**Constraints:**  
1 <= s1.size(), s2.size() <= 103  
Both strings may contain upper and lower case alphabets.

## Solution

```java

class Solution {
    
    public int longestCommonSubstr(String s1, String s2) {
        
        int n = s1.length();
        int m = s2.length();
        int max = 0;
        int[][] dp = new int[n + 1][m + 1];
        
        for (int i = 1; i <= n; i++) {
            for(int j = 1; j <= m; j++) {
                if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                    max = Math.max(max, dp[i][j]);
                } else {
                    dp[i][j] = 0;
                }
            }
        }
        
        return max;
    }
}

```