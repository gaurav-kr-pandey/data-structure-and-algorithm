### [Print all LCS sequences](https://www.geeksforgeeks.org/problems/print-all-lcs-sequences3413/1)

You are given two strings **s1** and **s2**. Your task is to print all **distinct** longest common subsequences in lexicographical order.

**Note:** A subsequence is derived from another string by deleting some or none of the elements without changing the order of the remaining elements.

**Examples:**

**Input:** s1 = "abaaa", s2 = "baabaca"
**Output:** ["aaaa", "abaa", "baaa"]  
**Explanation:** Length of **`lcs`** is 4, in lexicographical order they are "aaaa", "abaa", "baaa".

**Input:** s1 = "aaa", s2 = "a"
**Output:** ["a"]  
**Explanation:** Length of lcs is 1 and it is "a".

**Constraints:**  
1 ≤ s1.size(), s2.size() ≤ 50