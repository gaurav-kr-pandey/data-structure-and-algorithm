# 📘 Variable Size Sliding Window - DSA Notes

Sliding Window is a powerful technique for solving problems involving **contiguous subarrays** or substrings.

## 🧩 What is Variable Size Sliding Window?

Unlike **Fixed Size Sliding Window**, where window size `k` is known, **Variable Size Sliding Window** is used when:

- **The window size is not fixed**
- You need to **dynamically expand/shrink** the window based on a condition (e.g. no duplicate elements, at most K unique characters, sum <= X)
- Often used with **HashSet**, **HashMap**, or **counters** to track state inside the window

---

## 🧠 Core Idea

- Use **two pointers**: `i` (start), `j` (end)
- Grow window by incrementing `j`
- Shrink window from `i` when a constraint is violated
- Update result whenever constraints are satisfied

---

## 📌 General Template (Java Style)

```java
int i = 0, j = 0;
while (j < n) {

    // Step 1: Expand the window by including arr[j]
    //         Update frequency map, sum, or relevant DS
    //         Example: map.put(arr[j], map.getOrDefault(arr[j], 0) + 1);

    // Step 2: Shrink window until it becomes valid
    //         while (constraint violated) {
    //             remove arr[i] from window
    //             i++;
    //         }

    // Step 3: Update result based on window [i...j]
    //         if (constraint satisfied)
    //             result = update(result, j - i + 1, etc.)

    j++; // Always move right pointer
}
```

```java
int i = 0, j = 0;
while (j < n) {

	// keep adding till condition is met
    // expand the window

    while (condition violated) {
	    // Keep reducing till condition is not violated
        // shrink the window
        i++;
    }

    // process result
    j++;
}

```
