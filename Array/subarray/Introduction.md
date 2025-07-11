
### 🎯 Key Parameters

- **What is being asked**: sum, length, count, XOR, number of distinct integers, etc.
- **Constraints**: positive integers only, can include negative numbers, etc.
- **Fixed-size vs variable-size subarrays**

---

## 🔑 Patterns You Must Know

### **1. Fixed-size sliding window**

- **When?**: If array has **only positive integers** and you’re asked to find subarrays of **exact size** or **sum == k**.
- **Examples**:
    - Max sum subarray of size `k`.
- **Template**:

```java
int sum = 0, maxSum = 0;
int i = 0;
for (int j = 0; j < n; j++) {
    sum += arr[j];
    if (j - i + 1 == k) {
        maxSum = Math.max(maxSum, sum);
        sum -= arr[i];
        i++;
    }
}
```

---

### **2. Variable-size sliding window**

- **When?**: Array has only positives and you want **longest/shortest subarray with sum <=/== k**.
- **Trick**: Move `end` until valid, then `start` to shrink.
- **Example**: Longest subarray with sum ≤ `k` (positive numbers only).

---

### **3. Prefix sum with HashMap**

- **When?**: Negative numbers allowed, or you want to **count** subarrays with sum/XOR == k.
- **Idea**: Track prefixSum at every index.
    - If `prefixSum - k` exists in map, that means a subarray exists with sum = k.
    
- **Key**: `map.put(prefixSum, index/count)`
    
- **Examples**:
    - ✅ [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)
    - ✅ [Largest Subarray with 0 Sum](https://www.geeksforgeeks.org/problems/largest-subarray-with-0-sum/1)
    - ✅ [Count Subarrays with Given XOR](https://www.geeksforgeeks.org/problems/count-subarray-with-given-xor/1)

#### Template for Counting:

```java
Map<Integer, Integer> map = new HashMap<>();
map.put(0, 1); // base case

int count = 0, sum = 0;
for (int num : nums) {
    sum += num;
    if (map.containsKey(sum - k))
        count += map.get(sum - k);
    map.put(sum, map.getOrDefault(sum, 0) + 1);
}

```

---

### **4. Kadane’s Algorithm**

- **When?**: Find max sum subarray (including negative numbers).
- **Examples**:
    - ✅ Max subarray sum (LeetCode 53).
- **Template**:

```java
int maxSoFar = arr[0], currMax = arr[0];
for (int i = 1; i < arr.length; i++) {
    currMax = Math.max(arr[i], currMax + arr[i]);
    maxSoFar = Math.max(maxSoFar, currMax);
}
```

---

### **5. Frequency Map (for count of distinct elements)**

- **When?**: Count subarrays with **k distinct elements**, or **odd numbers**, etc.

- **Examples**:
    - ✅ [Count Number of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays/)
    - ✅ [Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers/)

#### Sliding Window Count Trick (at most K)

```java
int atMostK(int[] nums, int K) {
    Map<Integer, Integer> freq = new HashMap<>();
    int left = 0, count = 0;

    for (int right = 0; right < nums.length; right++) {
        freq.put(nums[right], freq.getOrDefault(nums[right], 0) + 1);
        if (freq.get(nums[right]) == 1) K--;

        while (K < 0) {
            freq.put(nums[left], freq.get(nums[left]) - 1);
            if (freq.get(nums[left]) == 0) K++;
            left++;
        }
        count += right - left + 1;
    }

    return count;
}

```

➡️ For exact K distinct: `atMostK(k) - atMostK(k-1)`

---

## 🧠 Intuition Building Tips

|Problem Goal|Data Structure / Approach|When to Use|
|---|---|---|
|Count subarrays (sum/k)|Prefix Sum + Map|Negative numbers involved|
|Largest subarray (sum=k)|Prefix Sum + Map|Need index for max length|
|Max subarray sum|Kadane’s|No specific k, just max sum|
|Count subarrays (XOR=k)|Prefix XOR + Map|XOR behaves like sum|
|K distinct elements|Sliding Window + Map|Count with constraints|
|Fixed size window|Basic window|Only positives, size fixed|

