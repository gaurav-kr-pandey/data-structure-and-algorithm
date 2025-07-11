---

---
---
**Practice:** [LeetCode](https://leetcode.com/problems/next-greater-element-i/description/) , [geeksforgeeks](https://www.geeksforgeeks.org/problems/next-larger-element-1587115620/1)

**Expected Approach: Using Stack - O(n) Time and O(n) Space**

> The idea is to use [stack](https://www.geeksforgeeks.org/stack-data-structure/) to find the **next greater element** by using the **Last-In-First-Out (LIFO) property.** We traverse the array from right to left. For each element, we remove elements from the stack that are **smaller than or equal** to it, as they cannot be the next greater element. If the stack is not empty after this, the top element of the stack is the next greater element for the current element. We then **push** the current element onto the stack.



```java
class Solution {
    public ArrayList<Integer> nextLargerElement(int[] arr) {
        
        Stack<Integer> st = new Stack<>();
        ArrayList<Integer> res = new ArrayList<>();
        int n = arr.length;
        
        for (int i = n - 1; i >= 0; i--) {
    
            while (!st.isEmpty() && st.peek() <= arr[i]) {
                st.pop();
            }
                
            int x = st.isEmpty() ? -1 : st.peek();
        
            st.add(arr[i]);            
            res.add(x);
        }
        
        Collections.reverse(res);
        
        return res;
    }
}
```


## Dry Run for Input:

`arr = [1, 2, 30, 40, 50, 60, 7, 8, 9]`

We go from **right to left**, so the logic is:  
For each element, find the first number to the right that is **greater**.

---

### Step-by-step Dry Run:

| Index | arr[i] | Stack Before        | Popped | Stack After            | Result (Before reverse) |
| ----- | ------ | ------------------- | ------ | ---------------------- | ----------------------- |
| 8     | 9      | []                  | —      | [9]                    | -1                      |
| 7     | 8      | [9]                 | —      | [9, 8]                 | 9                       |
| 6     | 7      | [9, 8]              | —      | [9, 8, 7]              | 8                       |
| 5     | 60     | [9, 8, 7]           | 7,8,9  | [60]                   | -1                      |
| 4     | 50     | [60]                | —      | [60, 50]               | 60                      |
| 3     | 40     | [60, 50]            | —      | [60, 50, 40]           | 50                      |
| 2     | 30     | [60, 50, 40]        | —      | [60, 50, 40, 30]       | 40                      |
| 1     | 2      | [60, 50, 40, 30]    | —      | [60, 50, 40, 30, 2]    | 30                      |
| 0     | 1      | [60, 50, 40, 30, 2] | —      | [60, 50, 40, 30, 2, 1] | 2                       |

### Result before reverse:

`[-1, 9, 8, -1, 60, 50, 40, 30, 2]`

### After reverse:

`[2, 30, 40, 50, 60, -1, 8, 9, -1]`

---

## Final Output:

`[2, 30, 40, 50, 60, -1, 8, 9, -1]`

---