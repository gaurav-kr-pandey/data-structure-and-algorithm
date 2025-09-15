## What is Fixed Size Sliding Window?

A technique where you analyze [[subarray]] or substrings of a **fixed length `k`** by sliding a window of size `k` over the array/string one element at a time.

---
## Why Use It?
Avoid recalculating results for overlapping subarrays and reduce time complexity from 

$O(n * k) \to O(n)$.

---
## Core Idea
- Compute result for the first window.
- Slide the window forward by removing the element going out and adding the element coming in.
---
## Visual Example

For `arr = [1, 3, -1, -3, 5, 3, 6, 7]` and `k = 3`:
Window indices: `0-2` -> `[1, 3, -1]`, `sum = 3`  
Slide: remove `1`, add `-3` -> `[3, -1, -3]`, sum updated

---
## Fixed Size Sliding Window Template

> In Sliding Window sometimes we need to use extra Data Structure, If using extra Data Structure (like **Deque** or **Queue**) then include step 1 else exclude it

#### Template:

```lisp
for (j ... n) {
	STEP 1: If using extra DS (like Deque or Queue)
			Remove elements out of window range (i.e., j - i + 1 > k)
			Remove elements based on problem e.g; smaller/larger than current
			Maintain state of DS
	STEP 2: Add current element to Window/DS
		    (e.g., add to sum, queue, deque, freq map etc.)
		if (window_size == k) {
			// window_size == j - i + 1
			STEP 3: When window size reaches 'k'
			        Calculate or update result
			        Remove i-th element from sum or DS
				    Slide window by incrementing 'i'
		}
	STEP 4: Expand window
}
```


```java
while (j < n) {

    /**
     * Step 1: If using extra DS (like Deque or Queue)
     *         - Remove elements out of window range (i.e., j - i + 1 > k)
     *         - Remove elements based on problem 
			       (e.g., smaller/larger than current)
     *         - Maintain state of DS
     */

    /** Step 2: Add current element to Window/DS
    *              (e.g., add to sum, queue, deque, freq map etc.)
	*/
	
    if (j - i + 1 == k) {
        /**
         * Step 3: When window size reaches 'k'
         *         - Calculate or update result
         *         - Remove i-th element from sum or DS
         *         - Slide window by incrementing 'i'
         */
        i++;
    }

    // Step 4: Expand window
    j++;
}
```


> If not using extra data structure (Deque, Queue etc.), remove that step


```lisp
for (j ... n) {
	STEP 1: (Not Required)
	STEP 2: Add current element to Window/DS
		    (e.g., add to sum, queue, deque, freq map etc.)
		
		if (window_size == k) {
			// window_size == j - i + 1
			STEP 3: When window size reaches 'k'
			        Calculate or update result
			        Remove i-th element from sum or DS
				    Slide window by incrementing 'i'
		}
	STEP 4: Expand window
}
```

```java
while (j < n) {

    // Step 2: Add current element to window/DS
    //         (e.g., add to sum, queue, deque, freq map etc.)

    if (j - i + 1 == k) {
        /**
         * Step 3: When window size reaches 'k'
         *         - Calculate or update result
         *         - Remove i-th element from sum or DS
         *         - Slide window by incrementing 'i'
         */
        i++;
    }

    // Step 4: Expand window
    j++;
}
```
## When to Use

Use this when you need to process **all subarrays/substrings of exact size `k`**, such as computing sum, max, min, count, or any aggregate.

---
## Use Cases & Variations

| Problem Type          | Description                          | Extra Data Structure Needed |
| --------------------- | ------------------------------------ | --------------------------- |
| Maximum/Minimum Sum   | Max/min sum of subarrays of size k   | None                        |
| First Negative Number | First negative number in each window | Queue                       |
| Maximum Element       | Max element in each window           | Deque                       |
| Count Even/Odd        | Count even or odd numbers in window  | None                        |
| Average               | Calculate average values             | None                        |

---

## Common Problems

| Problem                                          | Link                                                                                           |
| ------------------------------------------------ | ---------------------------------------------------------------------------------------------- |
| Maximum Average Subarray I                       | https://leetcode.com/problems/maximum-average-subarray-i/                                      |
| Sliding Window Maximum                           | https://leetcode.com/problems/sliding-window-maximum/                                          |
| First Negative Integer in Every Window of Size K | https://practice.geeksforgeeks.org/problems/first-negative-integer-in-every-window-of-size-k/0 |

---

## Common Mistakes & Fixes

| Mistake                              | Fix                                               |
| ------------------------------------ | ------------------------------------------------- |
| Incorrect window size check          | Always use `j - i + 1 == k`                       |
| Forgetting to shrink window          | Subtract `arr[i]` from sum and increment `i`      |
| Updating result before window formed | Update result only when window size equals `k`    |
| Ignoring edge cases                  | Handle cases like `k > arr.length` or empty array |

---

## Debugging Tips

- Print variables: `i`, `j`, current window elements, `sum`, and `result`
- Dry run on edge cases like:
    - `k = 1`
    - `k = arr.length`
    - All negative or all positive numbers
- Manually simulate sliding window movement with sample input
---
## Best Practices
- Maintain window size using `j - i + 1`
- Always shrink window after processing a full window
- Avoid recomputing sums by maintaining rolling sum
- Use appropriate data structures if problem requires more than sums (e.g., queues or deques)

## Interview Pattern Recognition

| Clue in Question                    | Likely Approach              |
| ----------------------------------- | ---------------------------- |
| “Subarray/substring of size k”      | Fixed size sliding window    |
| “Max/min in each window”            | Sliding window + deque       |
| “First negative/positive in window” | Sliding window + queue       |
| “Count occurrences in window”       | Fixed window logic           |
| “Length exactly k”                  | Two pointer window of size k |

## Fixed vs Variable Sliding Window

| Feature          | Fixed Size Window                    | Variable Size Window              |
| ---------------- | ------------------------------------ | --------------------------------- |
| Window size      | Constant `k`                         | Expands/shrinks dynamically       |
| Use cases        | Exact subarrays of length k          | Longest/shortest satisfying cond. |
| Pointer movement | Increment both `i` and `j` carefully | Expand `j`, shrink `i` as needed  |

## Summary

- Fixed size sliding window optimizes repeated computation on subarrays of length `k`.
- Use two pointers: `i` (start) and `j` (end) to maintain window.
- Expand window by increasing `j`, shrink by increasing `i` after processing full window.
- Maintain rolling sum or other aggregates for efficiency.
- Commonly used for max sum, min sum, counts, averages, and first negative element problems.