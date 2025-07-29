# 📚 Trie Data Structure (Prefix Tree) – Complete Notes

---

## 🔸 What is a Trie?

A **Trie** (pronounced as *try*), also known as a **Prefix Tree**, is a tree-like data structure used to store a dynamic set of strings, where each node represents a **single character** of a string.

- Used in **autocomplete**, **spell-checking**, **dictionary lookups**, and **IP routing**.
- Optimized for **prefix-based queries**.
- Common prefixes are **shared**, reducing redundancy.

---

## 🔧 Structure of a Trie Node

Each node typically contains:

- A `Map<Character, TrieNode>` or array of size 26 for children.
- A boolean `isEndOfWord` flag to mark valid end of a word.

```java
class TrieNode {
    Map<Character, TrieNode> children = new HashMap<>();
    boolean isEndOfWord = false;
}
```

---

## ✅ Supported Operations

### 1. Insert a Word

- Traverse each character.
- Create nodes if not present.
- Mark last node as end of word.

**Time Complexity:** `O(L)`  
**Space Complexity:** `O(L)` (worst case)

---

### 2. Search a Word

- Traverse character by character.
- If a character is missing → return `false`.
- Final node must have `isEndOfWord = true`.

**Time Complexity:** `O(L)`  
**Space Complexity:** `O(1)`

---

### 3. StartsWith (Prefix Search)

- Similar to search but no need to check `isEndOfWord`.

**Time Complexity:** `O(L)`

---

### 4. Delete a Word

- Traverse the word.
- Backtrack to delete unnecessary nodes.

**Time Complexity:** `O(L)`

---

### 5. Autocomplete Suggestions

- Reach the end of the prefix.
- Use DFS to collect all words under the node.

**Time Complexity:** `O(P + W)`  
Where `P = prefix length`, `W = number of words matched`

---

## 🔄 Trie vs HashMap/TreeMap

| Feature / Operation      | Trie                                   | HashMap / TreeMap                |
|--------------------------|----------------------------------------|----------------------------------|
| Key Type                 | Prefix-based, strings                  | Any type                         |
| Insert                   | O(L)                                   | O(1)/O(log N)                    |
| Search                   | O(L)                                   | O(1)/O(log N)                    |
| Prefix Search            | O(L)                                   | Not supported                    |
| Memory Usage             | Higher                                 | Lower                            |
| Autocomplete             | Easy                                   | Not feasible                     |
| Shared Prefix Storage    | Yes                                    | No                               |

---

## 🔴 Trade-offs and Requirements

- **Pros:**
  - Fast prefix and word lookups
  - Ideal for auto-suggestion engines
- **Cons:**
  - Higher memory usage
  - More complex implementation

---

## ✅ When to Use Trie?

- Large volume of strings with common prefixes
- Need for:
  - Prefix matching
  - Word suggestions
  - Efficient dictionary lookups

---

## 💻 Java Implementation – All Operations

```java
import java.util.*;

class TrieNode {
    Map<Character, TrieNode> children;
    boolean isEndOfWord;

    public TrieNode() {
        children = new HashMap<>();
        isEndOfWord = false;
    }
}

public class Trie {
    private final TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    // Insert a word
    public void insert(String word) {
        TrieNode node = root;
        for (char ch : word.toCharArray()) {
            node.children.putIfAbsent(ch, new TrieNode());
            node = node.children.get(ch);
        }
        node.isEndOfWord = true;
    }

    // Search a word
    public boolean search(String word) {
        TrieNode node = searchNode(word);
        return node != null && node.isEndOfWord;
    }

    // Prefix check
    public boolean startsWith(String prefix) {
        return searchNode(prefix) != null;
    }

    // Delete a word
    public boolean delete(String word) {
        return deleteHelper(root, word, 0);
    }

    private boolean deleteHelper(TrieNode node, String word, int index) {
        if (index == word.length()) {
            if (!node.isEndOfWord)
                return false;
            node.isEndOfWord = false;
            return node.children.isEmpty();
        }

        char ch = word.charAt(index);
        TrieNode child = node.children.get(ch);
        if (child == null)
            return false;

        boolean shouldDeleteCurrentNode = deleteHelper(child, word, index + 1);

        if (shouldDeleteCurrentNode) {
            node.children.remove(ch);
            return node.children.isEmpty() && !node.isEndOfWord;
        }

        return false;
    }

    // Autocomplete words starting with a prefix
    public List<String> getWordsStartingWith(String prefix) {
        TrieNode node = searchNode(prefix);
        List<String> result = new ArrayList<>();
        if (node != null) {
            collectWords(node, new StringBuilder(prefix), result);
        }
        return result;
    }

    private void collectWords(TrieNode node, StringBuilder path, List<String> result) {
        if (node.isEndOfWord) {
            result.add(path.toString());
        }

        for (Map.Entry<Character, TrieNode> entry : node.children.entrySet()) {
            path.append(entry.getKey());
            collectWords(entry.getValue(), path, result);
            path.deleteCharAt(path.length() - 1); // backtrack
        }
    }

    // Helper method
    private TrieNode searchNode(String prefix) {
        TrieNode node = root;
        for (char ch : prefix.toCharArray()) {
            node = node.children.get(ch);
            if (node == null)
                return null;
        }
        return node;
    }

    // Main for testing
    public static void main(String[] args) {
        Trie trie = new Trie();
        trie.insert("apple");
        trie.insert("app");
        trie.insert("application");
        trie.insert("banana");
        trie.insert("bat");

        System.out.println(trie.search("app"));           // true
        System.out.println(trie.startsWith("appl"));      // true
        System.out.println(trie.search("apply"));         // false

        trie.delete("app");
        System.out.println(trie.search("app"));           // false

        System.out.println(trie.getWordsStartingWith("app")); // [apple, application]
        System.out.println(trie.getWordsStartingWith("ba"));  // [banana, bat]
    }
}
```

---

## 📘 Extra

- Want to optimize for lowercase `a-z`? Replace `Map<Character, TrieNode>` with an array of size 26 for `children`.
- Use `children[ch - 'a']` for fast access and lower memory overhead.

---
