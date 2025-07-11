 
## 🔗 Problem Link

**LeetCode 560**: [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/)

> Given an integer array `nums` and an integer `k`, return the total number of subarrays whose sum equals to `k`.

---

## ❌ Brute Force Approach

### 🔧 Idea:

Check all subarrays and count those whose sum equals `k`.

### 💡 Code (O(n²)):

```java
public int subarraySum(int[] nums, int k) {
    int count = 0;
    for (int i = 0; i < nums.length; i++) {
        int sum = 0;
        for (int j = i; j < nums.length; j++) {
            sum += nums[j];
            if (sum == k) count++;
        }
    }
    return count;
}

```

### ⏱ Time: O(n²)

### 🧠 Space: O(1)

---

## ✅ Optimal Approach — Using Prefix Sum + HashMap

### 🔥 Intuition:

Let `prefixSum[j]` be the sum from `0` to `j`.  
If a subarray `i...j` has sum `k`, then:
```java
prefixSum[j] - prefixSum[i - 1] = k  
⇒ prefixSum[i - 1] = prefixSum[j] - k

```

We use a **HashMap** to count how many times each `prefixSum` has occurred so far.  
If `prefixSum - k` has occurred before, we found a subarray ending at current index with sum `k`

---

### 🔍 Example:

```java
nums = [1, 1, 1], k = 2

prefixSum = 0
map = {0:1} // base case
i=0: sum=1 → (1-2)= -1 not in map
i=1: sum=2 → (2-2)=  0 in map ⇒ count += 1
i=2: sum=3 → (3-2)=  1 in map ⇒ count += 1

Total = 2

```

---

## ✅ Java Code (O(n)):

```java
import java.util.HashMap;

public class SubarraySumEqualsK {
    public int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);  // Base case: empty prefix sum
        int count = 0;
        int prefixSum = 0;

        for (int num : nums) {
            prefixSum += num;
            // add the no. of time (prefixSum - k) has appeared beacuse that many way a new subarray will be created with sum k
            count += map.getOrDefault(prefixSum - k, 0);
            map.put(prefixSum, map.getOrDefault(prefixSum, 0) + 1);
        }

        return count;
    }
}

```

### ⏱ Time: O(n)

### 🧠 Space: O(n)

---

## 📎 Key Points

- `map.get(prefixSum - k)` counts how many times a subarray with sum `k` ends at current index.
- We store frequency of prefix sums to handle repeated values.
- Handles **negative numbers** correctly (unlike sliding window).
- Must initialize `map.put(0, 1)` to handle subarrays that start at index `0`.