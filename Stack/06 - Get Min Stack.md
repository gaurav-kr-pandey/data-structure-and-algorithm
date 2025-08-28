https://www.geeksforgeeks.org/problems/get-minimum-element-from-stack/1

Given **q** queries, You task is to implement the following **four** functions for a stack:
- **push(x) –** Insert an integer x onto the stack.
- **pop() –** Remove the top element from the stack.
- **peek() -** Return the top element from the stack. **If the stack is empty, return -1.**
- **getMin() –** Retrieve the minimum element from the stack in O(1) time. If the stack is empty, return -1.

Each query can be one of the following:
- **1 x** : Push x onto the stack.
- **2 :** Pop the top element from the stack.
- **3:** Return the top element from the stack. If the stack is empty, return -1.
- **4:** Return the minimum element from the stack.

## Intuition
We can use two stacks, to support -
Stack 1: `push`, `pop`, `peek`
Stack 2: `min`
	- push(x): where x <= stack2.peek()
	- pop(): stack1.peek() == stack2.peek()

### Solution 1: Using Extra Space - $O(2 * n)$

```java
class Solution {
    
    Deque<Integer> stack;
    Deque<Integer> minStack;
    
    public Solution() {
        stack = new ArrayDeque<>();
        minStack = new ArrayDeque<>();
    }

    public void push(int x) {
        if (minStack.isEmpty() || minStack.peek() >= x) {
            minStack.push(x);
        }
        stack.push(x);
    }

    public void pop() {
        if (!stack.isEmpty()) {
            int top = stack.peek(); // unboxing required for comparing Integer
            if (!minStack.isEmpty() && minStack.peek() == top) {
                minStack.pop();
            }
            stack.pop();
        }
    }

    public int peek() {
        return stack.isEmpty() ? -1 : stack.peek();
    }

        
    public int getMin() {
        return minStack.isEmpty() ? -1 : minStack.peek();
    }
}
```

##### Optimisation: Store Frequency of min variable to avoid duplicate-redundant entries in minStack:



### Solution 2: Without using supporting stack

We can store each value in pair(value, min);

```java
class Solution {
    
    Deque<int[]> stack;
    int min;
    
    public Solution() {
        stack = new ArrayDeque<>();
        min = Integer.MAX_VALUE;
    }

    public void push(int x) {
        min = Math.min(x, min);
        stack.push(new int[] {x, min});
    }

    public void pop() {
        if (!stack.isEmpty()) {
            int[] peek = stack.peek();
            stack.pop();
            if (min == peek[1]) {
                min = stack.isEmpty() ? Integer.MAX_VALUE : stack.peek()[1];
            }
        }
    }

    public int peek() {
        return stack.isEmpty() ? -1 : stack.peek()[0];
    }

        
    public int getMin() {
        return stack.isEmpty() || stack.peek()[1] == Integer.MAX_VALUE ? -1 : stack.peek()[1];
    }
}
```

### Solution 3: 
Instead of keeping a second stack, we **encode information about the min** inside the main stack.

**Logic:**
- Keep a single `stack` + an integer `minElement` that always stores the current minimum.
- When pushing a new element `x`:
    - If `x >= minElement`: push it normally.
    - If `x < minElement`: push a **modified value** `(2*x – minElement)` onto stack, and update `minElement = x`.
        - This encodes the previous min inside the pushed value.  
- When popping:
    - If `top >= minElement`: normal pop.
    - If `top < minElement`: it means the element was encoded. 

**Restore old min as :**

```java
2 * minElement – top
```

**Why it works:**  
That encoding ensures you can recover the previous minimum without keeping an entire minStack.


```java
class MinStackOptimized {

    Deque<Integer> stack;
    int minElement;

    public MinStackOptimized() {
        stack = new ArrayDeque<>();
        minElement = Integer.MAX_VALUE;
    }

    public void push(int x) {
        if (stack.isEmpty()) {
            stack.push(x);
            minElement = x;
        } else if (x >= minElement) {
            stack.push(x);
        } else {
            // encode the value
            stack.push(2 * x - minElement);
            minElement = x;
        }
    }

    public void pop() {
        if (stack.isEmpty()) return;
        int top = stack.pop();
        if (top < minElement) {
            // restore previous min
            minElement = 2 * minElement - top;
        }
        if (stack.isEmpty()) minElement = Integer.MAX_VALUE; // reset when empty
    }

    public int top() {
        if (stack.isEmpty()) return -1;
        int top = stack.peek();
        return (top < minElement) ? minElement : top;
    }

    public int getMin() {
        return stack.isEmpty() ? -1 : minElement;
    }
}

```