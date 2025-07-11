
# 🧠 Monotonic Stack - Go-To Notes

---

## 1. 🔹 Stack - Short Introduction

A **stack** is a linear data structure that follows the **LIFO (Last In First Out)** principle. Elements are added and removed only from the **top** of the stack.

### 📅 Core Stack Operations:

- `push(x)` → Add x to the top
- `pop()` → Remove and return the top
- `peek()` or `top()` → View the top without removing
- `isEmpty()` → Check if stack is empty

### 📊 Time Complexity:

All operations are **O(1)** on average.

---

## 2. 🤔 What is a Monotonic Stack?

A **Monotonic Stack** is a stack that is maintained in either **increasing** or **decreasing** order.

- **Monotonically Increasing Stack**: Elements **increase** from top to bottom.
    - Removes **larger or equal** elements.

- **Monotonically Decreasing Stack**: Elements **decrease** from top to bottom.
    - Removes **smaller or equal** elements.
        
> Useful for solving problems like: next greater element, stock span, temperature span, rectangle in histogram, etc.

### 📖 Usage Pattern

#### Step-by-Step:

1. **Choose traversal direction**:
    - Right to Left: When looking for next greater/smaller **to the right**
    - Left to Right: When looking for next greater/smaller **to the left**
        
2. **Choose stack type based on question**:

|Problem asks for|Stack Type|While condition|
|---|---|---|
|Next Greater|Monotonic Decreasing Stack|while (!st.isEmpty() && st.peek() <= val)|
|Next Smaller|Monotonic Increasing Stack|while (!st.isEmpty() && st.peek() >= val)|

3. **Decide whether to store value or index**:
    - Use index if the result needs positions/distance
    - Use value if the result only needs the element

---

## 3. 🔝 Very Important Monotonic Stack Problems

### ✅ Basic:

#### 1. **Next Greater Element (Right)**
- [LeetCode](https://leetcode.com/problems/next-greater-element-i/)
- [GFG](https://www.geeksforgeeks.org/problems/next-larger-element-1587115620/1)

#### 2. **Next Smaller Element (Right)**
- GFG: [https://www.geeksforgeeks.org/problems/next-smaller-element-5385628/1](https://www.geeksforgeeks.org/problems/next-smaller-element-5385628/1)

#### 3. **Stock Span Problem**
- GFG: [https://www.geeksforgeeks.org/problems/stock-span-problem-1587115621/1](https://www.geeksforgeeks.org/problems/stock-span-problem-1587115621/1)

#### 4. **Daily Temperatures**
- LeetCode: [https://leetcode.com/problems/daily-temperatures/](https://leetcode.com/problems/daily-temperatures/)


---

### 🔝 Intermediate:

#### 5. **Largest Rectangle in Histogram**

- LeetCode: [https://leetcode.com/problems/largest-rectangle-in-histogram/](https://leetcode.com/problems/largest-rectangle-in-histogram/)
- GFG: [https://www.geeksforgeeks.org/problems/largest-rectangle-in-histogram-1587115620/1](https://www.geeksforgeeks.org/problems/largest-rectangle-in-histogram-1587115620/1)

#### 6. **Trapping Rain Water**
- LeetCode: [https://leetcode.com/problems/trapping-rain-water/](https://leetcode.com/problems/trapping-rain-water/)
- GFG: [https://www.geeksforgeeks.org/problems/trapping-rain-water-1587115621/1](https://www.geeksforgeeks.org/problems/trapping-rain-water-1587115621/1)


---

### 🌟 Advanced:

#### 7. **Sum of Subarray Minimums**
- LeetCode: [https://leetcode.com/problems/sum-of-subarray-minimums/](https://leetcode.com/problems/sum-of-subarray-minimums/)

#### 8. **Maximal Rectangle** (in 2D Matrix)

- LeetCode: [https://leetcode.com/problems/maximal-rectangle/](https://leetcode.com/problems/maximal-rectangle/)

---

## 🏆 Tips to Master Monotonic Stack

- Think in terms of: "What am I trying to get rid of?"
- Remember: The **stack is a helper**, not the final result
- Annotate the stack manually during dry runs
- Practice tracing each push/pop operation

---

## 🔁 1. **Which Direction to Traverse? (Left → Right OR Right → Left)**

### ✅ General Rule:

|Problem Asks For|Direction|
|---|---|
|**Next Greater Element to the Right**|Right → Left 🔁|
|**Next Greater Element to the Left**|Left → Right ➡|
|**Next Smaller Element to the Right**|Right → Left 🔁|
|**Next Smaller Element to the Left**|Left → Right ➡|

> Always traverse **opposite** to the direction you’re answering for, so you can find it as you go.

---

## 🎯 2. **Store Index or Actual Value in Stack?**

### ✅ General Rule:

|If the result needs...|Store In Stack|
|---|---|
|Actual element values|Store values|
|Index-based answers (e.g., distances, positions)|Store **indices**|

**Example:**

- _"Find how many days until a warmer temperature" → Store index (to subtract positions)._
    
- _"Find next greater value" → Store actual value is enough._
    

---

## 🧠 3. **Check for Greater or Smaller Element?**

### ✅ General Rule:

|Question says...|Use Stack That Keeps...|While condition|
|---|---|---|
|**Next Greater** element|🟥 Monotonically Decreasing Stack|`while (!st.empty() && st.peek() <= arr[i])`|
|**Next Smaller** element|🟩 Monotonically Increasing Stack|`while (!st.empty() && st.peek() >= arr[i])`|

---

## 🧩 Putting It All Together

Let’s define a **decision framework**:

### ❓ Ask Yourself These:

1. **What are you trying to find?**
    
    - Next Greater or Smaller?
        
    - To the Left or Right?
        
2. **What should your answer return?**
    
    - The value? (store actual values)
        
    - The position/distance? (store indices)
        
3. **Choose your traversal direction**
    
    - Right → Left (for "next ... to the right")
        
    - Left → Right (for "next ... to the left")
        
4. **Choose your stack condition**
    
    - For Next Greater → Pop smaller/equal → Monotonically Decreasing
        
    - For Next Smaller → Pop larger/equal → Monotonically Increasing
        

---

## 🧪 Real Examples:

### ✅ Example 1: Next Greater Element to Right (Leetcode 496)

java

CopyEdit

`int[] nums = [4, 5, 2, 10, 8];`

> We want to find **next greater element to the right** for each element.

**➡ Traverse from right to left**  
**➡ Stack keeps decreasing elements**  
**➡ Store values (result is element, not index)**

java

CopyEdit

`while (!st.isEmpty() && st.peek() <= arr[i])     st.pop();`

---

### ✅ Example 2: Stock Span Problem

> For each day, find the number of consecutive previous days where the price was less than or equal to today.

**➡ Traverse from left to right**  
**➡ Stack keeps decreasing prices**  
**➡ Store **indices** (we need to calculate day gaps)**

java

CopyEdit

`while (!st.isEmpty() && price[st.peek()] <= price[i])     st.pop(); span[i] = st.empty() ? i + 1 : i - st.peek();`

---

## 📌 Final Cheat Sheet

|Task|Traverse|Stack Type|Stack Stores|Condition|
|---|---|---|---|---|
|Next Greater to Right|Right → Left|Monotonic Decreasing|Value|`st.peek() <= arr[i]`|
|Next Greater to Left|Left → Right|Monotonic Decreasing|Value|`st.peek() <= arr[i]`|
|Next Smaller to Right|Right → Left|Monotonic Increasing|Value|`st.peek() >= arr[i]`|
|Next Smaller to Left|Left → Right|Monotonic Increasing|Value|`st.peek() >= arr[i]`|
|Span Problems (index based)|Left → Right|Usually Decreasing|Index|depends on problem|

---

## 🧠 Mental Trick

- 🔺 **Next Greater → Pop smaller**
    
- 🔻 **Next Smaller → Pop greater**