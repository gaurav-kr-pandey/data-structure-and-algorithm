https://leetcode.com/problems/word-ladder/

A **transformation sequence** from word `beginWord` to word `endWord` using a dictionary `wordList` is a sequence of words `beginWord -> s1 -> s2 -> ... -> sk` such that:
- Every adjacent pair of words differs by a single letter.
- Every `si` for `1 <= i <= k` is in `wordList`. Note that `beginWord` does not need to be in `wordList`.
- `sk == endWord`

Given two words, `beginWord` and `endWord`, and a dictionary `wordList`, return _the **number of words** in the **shortest transformation sequence** from_ `beginWord` _to_ `endWord`_, or_ `0` _if no such sequence exists._

**Example 1:**
**Input:** beginWord = "hit", endWord = "cog", wordList = `["hot","dot","dog","lot","log"]`
**Output:** 0
**Explanation:** The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.

**Example 2:**
**Input:** beginWord = "hit", endWord = "cog", wordList = `["hot","dot","dog","lot","log","cog"]`
**Output:** 5
**Explanation:** One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.

### Approach:

This BFS traversal problem, we just need to try by replacing each character with every new character from `a --> z` and if exists in wordList then add it in the queue so that it will be our next move.

![[Pasted image 20250920191006.png]]
## Code:

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> words = new HashSet<>(wordList);
        if (!words.contains(endWord)) return 0;

        Queue<String> q = new LinkedList<>();
        q.offer(beginWord);
        int count = 1; // Start from 1 since beginWord is a valid transformation step

        while (!q.isEmpty()) {
            int size = q.size();
            while (size-- > 0) {
                String curr = q.poll();
                if (curr.equals(endWord)) return count;

                char[] arr = curr.toCharArray();
                for (int i = 0; i < arr.length; i++) {
                    char originalChar = arr[i];
                    for (char c = 'a'; c <= 'z'; c++) {
                        if (c == originalChar) continue;

                        arr[i] = c;
                        String next = new String(arr);
                        if (words.contains(next)) {
                            q.offer(next);
                            words.remove(next); // Mark as visited
                        }
                    }
                    arr[i] = originalChar; // Restore
                }
            }
            count++;
        }

        return 0;
    }
}
```


> Must try - Bi-Directional BFS to solve this -