---

---
---
**Practice:** [LeetCode](https://leetcode.com/problems/next-greater-element-i/description/) , [geeksforgeeks](https://www.geeksforgeeks.org/problems/next-larger-element-1587115620/1)

`Nearest Greater to Right | Next Largest Element`

**Expected Approach: Using Stack - O(n) Time and O(n) Space**
### 🔹 Intuition:
- You maintain a **monotonic decreasing stack** (values strictly decreasing top → bottom).
- When scanning from **right to left**, the stack always contains candidates for the "next greater".
- If an element is smaller than or equal to the current, it can’t be the "next greater", so you pop it.
- The top of the stack is the nearest greater element to the right.

## 🔄 Variants of the Problem

The beauty of this pattern is that **all four problems are just mirror images** depending on two choices:
1. **Direction of traversal** (Left-to-Right or Right-to-Left)
2. **Stack condition** (increasing or decreasing monotonic stack)

---
### 1. **Next Greater Element to Left (NGE Left)**
- **Traverse**: Left → Right
- **Maintain stack**: Monotonic decreasing (stack top > current)
- **Pop**: While stack top ≤ current
- **Answer**: Top of stack (if exists, else -1)

👉 This is just the "mirror image" of NGE Right.

---
### 2. **Next Smaller Element to Right (NSR)**
- **Traverse**: Right → Left
- **Maintain stack**: Monotonic increasing (stack top < current)
- **Pop**: While stack top ≥ current
- **Answer**: Top of stack (if exists, else -1)

---
### 3. **Next Smaller Element to Left (NSL)**
- **Traverse**: Left → Right
- **Maintain stack**: Monotonic increasing (stack top < current)
- **Pop**: While stack top ≥ current
- **Answer**: Top of stack (if exists, else -1)

---
## 🧠 Unified Intuition (How to Think Fast)
Whenever you see "Next ___ Element ___":
- **Greater / Smaller** decides **monotonic stack type**:
    - Greater → Decreasing stack
    - Smaller → Increasing stack

- **Left / Right** decides **direction of traversal**:
    - Left → Left → Right
    - Right → Right → Left

## Summary Table:
| Problem   | Traverse     | Stack Type | Condition (pop while…) |
| --------- | ------------ | ---------- | ---------------------- |
| NGE Right | Right → Left | Decreasing | stack.top ≤ curr       |
| NGE Left  | Left → Right | Decreasing | stack.top ≤ curr       |
| NSE Right | Right → Left | Increasing | stack.top ≥ curr       |
| NSE Left  | Left → Right | Increasing | stack.top ≥ curr       |
👉 All four are **O(n) time, O(n) space**.

### 🔹 Time Complexity:
- Each element is **pushed once** and **popped at most once** → `O(n)`.
- The `Collections.reverse()` is `O(n)`.  
    ➡️ Total = **O(n)**
### 🔹 Space Complexity:
- Stack stores at most `n` elements → `O(n)`.
- Result list stores `n` results → `O(n)`.  
    ➡️ Overall = **O(n)**

### Code:


```java
class MonotonicStackPatterns {

    // Next Greater Element to Right
    public static int[] nextGreaterRight(int[] arr) {
        int n = arr.length;
        int[] res = new int[n];
        Deque<Integer> st = new ArrayDeque<>();

        for (int i = n - 1; i >= 0; i--) {
            while (!st.isEmpty() && st.peek() <= arr[i]) st.pop();
            res[i] = st.isEmpty() ? -1 : st.peek();
            st.push(arr[i]);
        }
        return res;
    }

    // Next Greater Element to Left
    public static int[] nextGreaterLeft(int[] arr) {
        int n = arr.length;
        int[] res = new int[n];
        Deque<Integer> st = new ArrayDeque<>();

        for (int i = 0; i < n; i++) {
            while (!st.isEmpty() && st.peek() <= arr[i]) st.pop();
            res[i] = st.isEmpty() ? -1 : st.peek();
            st.push(arr[i]);
        }
        return res;
    }

    // Next Smaller Element to Right
    public static int[] nextSmallerRight(int[] arr) {
        int n = arr.length;
        int[] res = new int[n];
        Deque<Integer> st = new ArrayDeque<>();

        for (int i = n - 1; i >= 0; i--) {
            while (!st.isEmpty() && st.peek() >= arr[i]) st.pop();
            res[i] = st.isEmpty() ? -1 : st.peek();
            st.push(arr[i]);
        }
        return res;
    }

    // Next Smaller Element to Left
    public static int[] nextSmallerLeft(int[] arr) {
        int n = arr.length;
        int[] res = new int[n];
        Deque<Integer> st = new ArrayDeque<>();

        for (int i = 0; i < n; i++) {
            while (!st.isEmpty() && st.peek() >= arr[i]) st.pop();
            res[i] = st.isEmpty() ? -1 : st.peek();
            st.push(arr[i]);
        }
        return res;
    }
}
```

