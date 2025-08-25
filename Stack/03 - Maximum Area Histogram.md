https://www.geeksforgeeks.org/problems/maximum-rectangular-area-in-a-histogram-1587115620/1

You are given a **histogram** represented by an array **arr**, where each element of the array denotes the **height** of the bars in the histogram. All bars have the same **width of 1 unit**.
Your task is to find the **largest** rectangular area possible in the given histogram, where the rectangle can be formed using a number of contiguous bars.

**Input:** `arr[] = [60, 20, 50, 40, 10, 50, 60]`
 
![Largest-Rectangular-Area-in-a-Histogram](https://media.geeksforgeeks.org/wp-content/uploads/20240924161857/Largest-Rectangular-Area-in-a-Histogram.webp)

**Output:** 100
**Explanation:** We get the maximum by picking bars highlighted above in green (50, and 60). The area is computed (smallest height) * (no. of the picked bars) = 50 * 2 = 100.

### Intuition:

**How to calculate histogram for every index `arr[i]` ?**
For example above - 
`arr[] = [60, 20, 50, 40, 10, 50, 60]`
`index = [00, 01, 02, 03, 04, 05, 06]`

Let's look for index `3` , 
`index3` -  `((4 - 1) - 1) * arr[3]`, where 
	`4 ` - index of next smaller element to right
	`1 ` - index of next smaller element to left
	`-1` - We need histogram `40, 50` with length `2` but `4 - 1` is giving `3` hence we need to decrement it by `-1`.

So, formula derived is:
```java
area(i) => 
([index of next smaller to right] - [index of next smaller to left] - 1) * arr[i]
```

**What if there is no greater element to left/right?**
To satisfy the formula, we need these two value, hence if we do not have either of them we will take following values as default option:
```lisp
	nseIndex left  --> -1
	nseIndex right --> arr.length + 1
```

**Code:**

```java
class Solution {
    public int getMaxArea(int[] arr) {
        int n = arr.length;
        int[] left = getNextSmallerToLeft(arr);
        int[] right = getNextSmallerToRight(arr);
        
        int maxArea = 0;
        for (int i = 0; i < n; i++) {
            int width = right[i] - left[i] - 1;
            int area = arr[i] * width;
            maxArea = Math.max(maxArea, area);
        }
        return maxArea;
    }
    
    int[] getNextSmallerToLeft(int[] arr) {
        int n = arr.length;
        int[] result = new int[n];
        Deque<Integer> stack = new ArrayDeque<>();
        
        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && arr[stack.peek()] >= arr[i]) {
                stack.pop();
            }
            result[i] = stack.isEmpty() ? -1 : stack.peek();
            stack.push(i);
        }
        return result;
    }
    
    int[] getNextSmallerToRight(int[] arr) {
        int n = arr.length;
        int[] result = new int[n];
        Deque<Integer> stack = new ArrayDeque<>();
        
        for (int i = n - 1; i >= 0; i--) {
            while (!stack.isEmpty() && arr[stack.peek()] >= arr[i]) {
                stack.pop();
            }
            result[i] = stack.isEmpty() ? n : stack.peek();
            stack.push(i);
        }
        return result;
    }
}
```

### Steps
1. Compute **Next Smaller to Left (NSL)** → O(n)
2. Compute **Next Smaller to Right (NSR)** → O(n)
3. Loop over array to calculate area → O(n)

Each element is pushed/popped from stack at most once.

**Time Complexity:** $O(n)$
- NSL: O(n)
- NSR: O(n)
- Area loop: O(n)

**Space Complexity:** $O(n)$
- NSL array: O(n)
- NSR array: O(n)
- Stack: O(n) (worst case: increasing heights like `[1,2,3,4,...]`)
### Can we optimise it for $O(n)$ space complexity ?

Now, what if we don’t explicitly store **NSL** and **NSR**?
- Notice that in Version 1, we first computed **NSL** and then later used it while iterating.
- Similarly for **NSR**, we computed ahead of time.

👉 But in practice, we don’t need to know **all NSR values in advance**.  
We only need the NSR **at the moment we encounter it**.

---
### 🧩 Key Idea

When iterating left → right:
- If the current bar `heights[i]` is **taller** than the bar at the stack’s top:  
    → We push `i` (because we can extend rectangles).
- If the current bar `heights[i]` is **shorter** than the bar at the stack’s top:  
    → This means we’ve just found the **NSR** for the top of the stack!
Why?
- The current bar `heights[i]` acts as a **right boundary** (smaller element).
- The previous element in the stack (after popping) acts as a **left boundary**.

So, at the moment of popping:
- **height** = `heights[stack.pop()]`
- **right boundary** = `i` (current index)
- **left boundary** = stack.peek() (after popping)
- **width** = `i - stack.peek() - 1`
- **area** = height × width

> **Note:**
> We can omit extra space by using following code:

```java
class Solution {
    public static int getMaxArea(int[] heights) {
        int n = heights.length;
        Deque<Integer> stack = new ArrayDeque<>();
        int maxArea = 0;

        for (int i = 0; i <= n; i++) {
            int currHeight = (i == n) ? 0 : heights[i]; // sentinel
            while (!stack.isEmpty() && currHeight < heights[stack.peek()]) {
                int height = heights[stack.pop()];
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                maxArea = Math.max(maxArea, height * width);
            }
            stack.push(i);
        }
        return maxArea;
    }
}
```

### Steps
1. Iterate over array with one pass (plus sentinel `0` at the end).
2. Maintain stack of indices.
3. For each element, while stack is not empty and current height is smaller → pop & compute area.
    - This pop gives both **NSL (from stack)** and **NSR (current index)** implicitly.
### ⏱️ Time Complexity
- Each element is **pushed once** and **popped once**.
- Inner `while` loop across entire run is amortized O(n).
- **Total = O(n)**

👉 Same as Version 1, but without extra arrays.
### 💾 Space Complexity
- Stack: O(n) (worst case strictly increasing array like `[1,2,3,4,5]`)
- No extra NSL/NSR arrays.
- **Total = O(n)**

| Aspect                   | Version 1 (Two Arrays + Stack) | Version 2 (One-Pass + Stack)              |
| ------------------------ | ------------------------------ | ----------------------------------------- |
| **Time Complexity**      | O(n)                           | O(n)                                      |
| **Extra Space (arrays)** | O(2n) (NSL + NSR)              | 0                                         |
| **Stack Space**          | O(n)                           | O(n)                                      |
| **Total Space**          | O(n) + O(2n) = O(n)            | O(n)                                      |
| **Implementation**       | Easier to reason about         | Cleaner, more concise, interview standard |