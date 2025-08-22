
# 🗂️ Stack Problem Reference

## 📌 Java Stack Utilities
```java
// Stack Class
Stack<Integer> st = new Stack<>();
st.push(10);        // insert
st.pop();           // remove top
st.peek();          // check top
st.isEmpty();       // check empty

// ArrayDeque (preferred for performance)
Deque<Integer> dq = new ArrayDeque<>();
dq.push(10);
dq.pop();
dq.peek();
```

⚡ Use `ArrayDeque` instead of Stack in CP for better performance  

---

## 🔑 Common Stack Patterns  

### 1. Balanced Parentheses
```java
public boolean isValid(String s) {
    Deque<Character> st = new ArrayDeque<>();
    for (char c : s.toCharArray()) {
        if (c == '(' || c == '[' || c == '{') st.push(c);
        else {
            if (st.isEmpty()) return false;
            char top = st.pop();
            if ((c == ')' && top != '(') || 
                (c == ']' && top != '[') || 
                (c == '}' && top != '{')) return false;
        }
    }
    return st.isEmpty();
}
```

---

### 2. Next Greater Element (Monotonic Stack)
```java
public int[] nextGreater(int[] nums) {
    int n = nums.length;
    int[] res = new int[n];
    Arrays.fill(res, -1);
    Deque<Integer> st = new ArrayDeque<>();
    for (int i = 0; i < n; i++) {
        while (!st.isEmpty() && nums[st.peek()] < nums[i]) {
            res[st.pop()] = nums[i];
        }
        st.push(i);
    }
    return res;
}
```

---

### 3. Largest Rectangle in Histogram
```java
public int largestRectangleArea(int[] heights) {
    int n = heights.length, max = 0;
    Deque<Integer> st = new ArrayDeque<>();
    for (int i = 0; i <= n; i++) {
        int h = (i == n ? 0 : heights[i]);
        while (!st.isEmpty() && h < heights[st.peek()]) {
            int height = heights[st.pop()];
            int left = st.isEmpty() ? -1 : st.peek();
            max = Math.max(max, height * (i - left - 1));
        }
        st.push(i);
    }
    return max;
}
```

---

### 4. Min Stack
```java
class MinStack {
    Deque<Integer> st = new ArrayDeque<>();
    Deque<Integer> minSt = new ArrayDeque<>();

    public void push(int x) {
        st.push(x);
        if (minSt.isEmpty() || x <= minSt.peek()) minSt.push(x);
    }

    public void pop() {
        if (st.peek().equals(minSt.peek())) minSt.pop();
        st.pop();
    }

    public int top() { return st.peek(); }
    public int getMin() { return minSt.peek(); }
}
```

---

### 5. Daily Temperatures
```java
public int[] dailyTemperatures(int[] temp) {
    int n = temp.length;
    int[] ans = new int[n];
    Deque<Integer> st = new ArrayDeque<>();
    for (int i = 0; i < n; i++) {
        while (!st.isEmpty() && temp[st.peek()] < temp[i]) {
            int idx = st.pop();
            ans[idx] = i - idx;
        }
        st.push(i);
    }
    return ans;
}
```

---

### 6. Evaluate Reverse Polish Notation
```java
public int evalRPN(String[] tokens) {
    Deque<Integer> st = new ArrayDeque<>();
    for (String t : tokens) {
        if ("+-*/".contains(t)) {
            int b = st.pop(), a = st.pop();
            switch (t) {
                case "+": st.push(a + b); break;
                case "-": st.push(a - b); break;
                case "*": st.push(a * b); break;
                case "/": st.push(a / b); break;
            }
        } else {
            st.push(Integer.parseInt(t));
        }
    }
    return st.pop();
}
```

---

### 7. Trapping Rain Water
```java
public int trap(int[] height) {
    int n = height.length, ans = 0;
    Deque<Integer> st = new ArrayDeque<>();
    for (int i = 0; i < n; i++) {
        while (!st.isEmpty() && height[i] > height[st.peek()]) {
            int top = st.pop();
            if (st.isEmpty()) break;
            int dist = i - st.peek() - 1;
            int bounded = Math.min(height[i], height[st.peek()]) - height[top];
            ans += dist * bounded;
        }
        st.push(i);
    }
    return ans;
}
```

---

## 📚 Classic Problem Categories
- Parentheses / Expression Problems  
- Monotonic Stack Problems (NGE, Daily Temps, Histogram, Rain Water)  
- Min/Max Stack  
- Queue/Stack Implementations  
- Path / String Decoding Problems  

---

## 🚀 Tips for Stack Problems
- Think "Last Unresolved Item" → Use Stack  
- For range queries (left/right span) → use Monotonic Stack  
- For expression parsing → stack for operators + operands  
- Decide carefully: store value OR index in stack  
- Sometimes two stacks simplify design (MinStack, Queue via Stacks)  

