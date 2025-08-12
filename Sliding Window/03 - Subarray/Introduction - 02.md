# 📘 Subarray Problem Cheatsheet – Patterns vs Techniques

---

## 🔹 1. Sliding Window

### ✅ Use When:
- Array has only **positive numbers**
- You want subarrays of:
    - **fixed length**
    - **at most/exactly K conditions** (odd, even, distinct, etc.)

### 🧠 Variants:
- Fixed Window Size
- Variable Window Size
- Count of subarrays with at most K conditions
- 
### 🔧 Template: Variable window size

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

### ✅ Example Problems:

- Count subarrays with at most k odd numbers
- Subarrays with k distinct integers
- Longest subarray with sum ≤ K (positive only)

---

## 🔹 2. Prefix Sum + HashMap

### ✅ Use When:

- Array can have **negative numbers**
- Find:
    - Count of subarrays with **sum = K**
    - **Longest subarray** with sum = K    
    - Subarray with **0 sum**  (or with sum k)
### 🧠 Variants:
- `Map<sum, count>` → count of subarrays
- `Map<sum, index>` → length of subarray

### 🔧 Template: Count of subarrays with sum = k

```java
Map<Integer, Integer> map = new HashMap<>();
map.put(0, 1);
int sum = 0, count = 0;

for (int num : nums) {
    sum += num;
    count += map.getOrDefault(sum - k, 0);
    map.put(sum, map.getOrDefault(sum, 0) + 1);
}

```

### 🔧 Template: Longest subarray with sum = k
```java
Map<Integer, Integer> map = new HashMap<>();
map.put(0, -1);
int sum = 0, maxLen = 0;

for (int i = 0; i < nums.length; i++) {
    sum += nums[i];
    if (map.containsKey(sum - k)) {
        maxLen = Math.max(maxLen, i - map.get(sum - k));
    }
    map.putIfAbsent(sum, i);
}

```

### ✅ Example Problems:

- Subarray sum equals K (Leetcode)
- Largest subarray with 0 sum (GFG)
- Longest subarray with sum = K

---

## 🔹 3. Prefix XOR + HashMap

### ✅ Use When:

- Problem involves **XOR of subarray**

### 🔧 Template: Count of subarrays with XOR = k
```java
Map<Integer, Integer> map = new HashMap<>();
map.put(0, 1);
int xor = 0, count = 0;

for (int num : nums) {
    xor ^= num;
    count += map.getOrDefault(xor ^ k, 0);
    map.put(xor, map.getOrDefault(xor, 0) + 1);
}

```

### ✅ Example Problems:

- Count subarrays with given XOR (GFG)

---

## 🔹 4. Kadane's Algorithm

### ✅ Use When:

- Problem is: **Maximum subarray sum**

### 🔧 Template:
```java
int maxSum = nums[0], currSum = nums[0];

for (int i = 1; i < nums.length; i++) {
    currSum = Math.max(nums[i], currSum + nums[i]);
    maxSum = Math.max(maxSum, currSum);
}

```

### ✅ Example Problems:

- Maximum subarray (Leetcode)
---
## 🔹 5. Difference of Counts (Sliding Window)

### ✅ Use When:

- Problem asks for **exactly K** conditions (distinct/odd/even)
	`exactlyK = atMost(K) - atMost(K - 1)`

### 🔧 Template: Subarrays with exactly K distinct elements

```java
int atMostK(int[] nums, int k) {
    int i = 0, res = 0;
    Map<Integer, Integer> map = new HashMap<>();

    for (int j = 0; j < nums.length; j++) {
        map.put(nums[j], map.getOrDefault(nums[j], 0) + 1);

        while (map.size() > k) {
            map.put(nums[i], map.get(nums[i]) - 1);
            if (map.get(nums[i]) == 0) map.remove(nums[i]);
            i++;
        }

        res += j - i + 1;
    }
    return res;
}

int exactlyK(int[] nums, int k) {
    return atMostK(nums, k) - atMostK(nums, k - 1);
}

```

### ✅ Example Problems:

- Subarrays with k distinct integers (Leetcode)
- Nice subarrays (odd count = exactly K)

---

## 🔹 6. Other Patterns (Rare but Useful)

|Pattern|Use Case|Template Idea|
|---|---|---|
|Two Pointers|Sorted arrays, pair sum problems|i++, j--|
|Binary Search on Answer|Min/Max subarray length under constraint|Use sliding window inside check function|

---

## 🔄 Summary Table

| Problem Type                            | Technique                      | What to Store in Map |
| --------------------------------------- | ------------------------------ | -------------------- |
| Count subarrays with sum = K            | Prefix Sum                     | sum → freq           |
| Longest subarray with sum = K           | Prefix Sum                     | sum → index          |
| Count subarrays with XOR = K            | Prefix XOR                     | xor → freq           |
| Maximum subarray sum                    | Kadane's                       | —                    |
| Count subarrays with at most K distinct | Sliding Window                 | freq map             |
| Exactly K (odd/distinct) subarrays      | Trick: atMost(k) - atMost(k-1) | Call function twice  |