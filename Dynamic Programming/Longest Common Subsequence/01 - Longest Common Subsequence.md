### [Longest Common Subsequence](https://www.geeksforgeeks.org/problems/longest-common-subsequence-1587115620/1)

Given two strings **`s1`** and **`s2`**, return the length of their **longest common subsequence** (LCS). If there is no common subsequence, return **0**.

_A subsequence is a sequence that can be derived from the given string by deleting some or no elements without changing the order of the remaining elements. For example, "ABE" is a subsequence of "ABCDE"._

**Examples:**

**Input:** s1 = "ABCDGH", s2 = "AEDFHR"
**Output:** 3
**Explanation:** The longest common subsequence of "ABCDGH" and "AEDFHR" is "ADH", which has a length of 3.

**Input:** s1 = "ABC", s2 = "AC"
**Output:** 2
**Explanation:** The longest common subsequence of "ABC" and "AC" is "AC", which has a length of 2.

**Input:** s1 = "XYZW", s2 = "XYWZ"
**Output:** 3
**Explanation:** The longest common subsequences of "XYZW" and "XYWZ" are "XYZ" and "XYW", both of length 3.

**Constraints:**  
1<= s1.size(), s2.size() <=103  
Both strings s1 and s2 contain only uppercase English letters.

## Solution

```java

class Solution {
    static int lcs(String s1, String s2) {
        int n = s1.length(), m = s2.length();
        char[] arr1 = s1.toCharArray();
        char[] arr2 = s2.toCharArray();
        Integer[][] dp = new Integer[n + 1][m + 1];
        return lcs(arr1, arr2, dp, n, m);
    }
    
    static int lcs(char[] s1, char[] s2, Integer[][] dp, int n, int m) {
        if (n == 0 || m == 0) {
            return 0;
        }
        
        if (dp[n][m] != null) {
            return dp[n][m];
        }
        
        if (s1[n - 1] == s2[m - 1]) {
            dp[n][m] = 1 + lcs(s1, s2, dp, n - 1, m - 1);
        } else {
            dp[n][m] = Math.max(lcs(s1, s2, dp, n - 1, m), lcs(s1, s2, dp, n, m - 1));
        }
        
        return dp[n][m];
    }
}

```