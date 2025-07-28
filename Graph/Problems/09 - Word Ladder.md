https://leetcode.com/problems/word-ladder/

### Approach:

This BFS traversal problem, we just need to try every new character and if exists in wordList it can be out next move.


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