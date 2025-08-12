https://www.geeksforgeeks.org/problems/count-occurences-of-anagrams5839/1

Given a word **pat** and a text **txt**. Return the count of the occurrences of anagrams of the word in the text.

**Example 1:**
**Input:** txt = "forxxorfxdofr", pat = "for"
**Output:** 3
**Explanation:** **for, orf** and **ofr** appears in the **txt,** hence answer is 3.

### Solution:

```java
class Solution {

    int search(String pat, String txt) {
        
        int n = pat.length(), m = txt.length();
        int i = 0, j = 0, count = 0;
        int[] arr1 = new int[26];
        int[] arr2 = new int[26];

        for (char c: pat.toCharArray()) {
            arr1[c - 'a']++;
        }
        
        while (j < m) {
            arr2[txt.charAt(j) - 'a']++;
            
            if (j - i + 1 == n) {
                if (Arrays.equals(arr1, arr2)) {
                    count++;
                }
                arr2[txt.charAt(i) - 'a']--;
                i++;
            }
            
            j++;
        }
        
        return count;
    }
}
```