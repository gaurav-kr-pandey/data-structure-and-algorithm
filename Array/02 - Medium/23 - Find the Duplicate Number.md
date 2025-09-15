https://leetcode.com/problems/find-the-duplicate-number/description/

Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.
There is only **one repeated number** in `nums`, return _this repeated number_.
You must solve the problem **without** modifying the array `nums` and using only constant extra space.

**Example 1:**
**Input:** `nums` = `[1,3,4,2,2]`
**Output:** 2

## Intuition:

- We start with $O(n^2)$ solution, we search for same element on rest of the array, if found return element.
- We can also sort the array and check for two adjacent elements are equals or not. $O(n * log(n))$
- We can also use `SET` to store all the elements and check existence. Space: $O(n)$, Time: $O(n)$

The optimal solution is **Floyd’s Tortoise and Hare (cycle detection)** used on the array as if it were a linked list. It runs in **O(n)** time and **O(1)** extra space and does **not** modify the input array. 

#### Why cycle detection works ?

- You're given `nums` of length `n + 1` with values in `1....n`. Because there are `n + 1` items but only `n` possible values, a value must repeat.
- Treat array indices and values as pointers: from index `i` jump to `nums[i]`. That is, define a function `f(i) = nums[i]`. Starting from index `0` and repeatedly applying `f` forms a sequence of indices.
- Because values are in `1....n` (not `0` necessarily), every jump (after the first) goes to an index in `1....n`. The pigeonhole principle guarantees there must be a cycle in this graph — the duplicate value is the entry point of that cycle.
- Floyd’s algorithm finds the meeting point inside the cycle. Reset one pointer to the start index (`0`) and move both pointers one step at a time; they will meet at the cycle entry, which is the duplicate number.

## Code:

```java
class Solution {
    public int findDuplicate(int[] nums) {
        int fast = nums[0];
        int slow = nums[0];

        do {
            fast = nums[nums[fast]];
            slow = nums[slow];
        } while (fast != slow);

        fast = nums[0];
        while (fast != slow) {
            fast = nums[fast];
            slow = nums[slow];
        }

        return fast;
    }
}
```

### Complexity
- Time: **O(n)** - each pointer advances at most a constant multiple of `n`.
- Space: **O(1)** extra.