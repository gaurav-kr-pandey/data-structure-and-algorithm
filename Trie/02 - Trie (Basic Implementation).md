https://leetcode.com/problems/implement-trie-prefix-tree/description/

### Code:

```java
class Trie {
    class TrieNode {
        TrieNode[] childrens;
        boolean isEndOfWord;

        public TrieNode() {
            childrens = new TrieNode[26];
            isEndOfWord = false;
        }

        public boolean isEmpty(char key) {
            return childrens[key - 'a'] ==  null;
        }

        public TrieNode get(char key) {
            return childrens[key - 'a'];
        }

        public void add(char key) {
            if (isEmpty(key)) {
                childrens[key - 'a'] = new TrieNode();
            }
        }

        public void setEnd(boolean isEnd) {
            isEndOfWord = isEnd;
        }

        public boolean isEnd() {
            return isEndOfWord;
        }
    }

    private final TrieNode root;
    public Trie() {
        root = new TrieNode();
    }
    
    public void insert(String word) {
        char[] arr = word.toCharArray();
        TrieNode curr = root;
        for (int i = 0; i < arr.length; i++) {
            if (curr.isEmpty(arr[i])) {
                curr.add(arr[i]);
            }
            curr = curr.get(arr[i]);
        }
        curr.setEnd(true);
    }
    
    public boolean search(String word) {
        char[] arr = word.toCharArray();
        TrieNode curr = root;
        for (int i = 0; i < arr.length; i++) {
            if (curr.isEmpty(arr[i])) {
                return false;
            }
            curr = curr.get(arr[i]);
        }
        return curr.isEnd();
    }
    
    public boolean startsWith(String prefix) {
        char[] arr = prefix.toCharArray();
        TrieNode curr = root;
        for (int i = 0; i < arr.length; i++) {
            if (curr.isEmpty(arr[i])) {
                return false;
            }
            curr = curr.get(arr[i]);
        }
        return true;
    }
}
```