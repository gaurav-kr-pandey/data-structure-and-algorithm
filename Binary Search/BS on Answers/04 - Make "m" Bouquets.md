https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/description/

**You are given:**
1. An array `bloomDay[]`, where `bloomDay[i]` means **the day on which the** `i`-th **flower will bloom**.
2. Two integers:
    - `m` = the number of **bouquets** you want to make.
    - `k` = the number of **flowers needed per bouquet**.

**Bouquet rule:**
- A bouquet must be made from **k adjacent flowers** in the garden (contiguous in the array).
- You can only use a flower **after its bloomDay has passed or on that exact day**.

**Goal:**  
Find the **minimum number of days** needed so that you can make at least `m` bouquets.  
If it is impossible to make `m` bouquets (because not enough flowers), return `-1`.

**Explanation:**

 **What does `bloomDay[i]` mean?**
- It does **not** mean you can pick flowers on every day.
- It means the flower planted at position `i` (think: garden bed at index `i`) will **bloom exactly once, on that day**, and then it stays bloomed forever after.
- So each index in the array corresponds to **one fixed flower** in the garden.
**What does `m` mean?**
- `m` is the **number of bouquets** you must form in total.
**What does `k` mean?**
- Each bouquet requires **k flowers that are adjacent in the garden** (adjacent indices).
- Example: if `k=3`, then valid bouquets are `[i, i+1, i+2]` (contiguous positions).
So `k` is not a number of days. It’s the **bouquet size** in terms of flowers.
**Key Clarification**
- You do **not** “pick one flower per day”.
- You “wait until some day D”, and then look at the array:
    - If `bloomDay[i] ≤ D`, that flower is bloomed and available.
    - If `bloomDay[i] > D`, that flower isn’t available yet.
- Then, from the available flowers, you check: can I group them into at least `m` bouquets of size `k` (each group must be adjacent)?

### Intuition:



**Code:**

```java
class Solution {
    public int minDays(int[] bloomDay, int m, int k) {
        int n = bloomDay.length;
        int ans = -1;

        // Edge case: not enough flowers at all
        if ((long)m * k > n) return -1;

        // Binary search boundaries:
        // earliest flower bloom to the latest bloom
        int low = Arrays.stream(bloomDay).min().getAsInt();
        int high = Arrays.stream(bloomDay).max().getAsInt();

        // Binary Search on the number of days
        while (low <= high) {
            int mid = low + (high - low) / 2; // candidate day

            if (isPossible(bloomDay, m, k, mid)) {
                ans = mid;        // possible, store answer
                high = mid - 1;   // but try to find smaller day
            } else {
                low = mid + 1;    // not possible, need more days
            }
        }

        return ans;
    }

    // Check if we can make m bouquets by waiting until 'day'
    private boolean isPossible(int[] arr, int m, int k, int day) {
        int consecutive = 0; // consecutive bloomed flowers
        int bouquets = 0;    // number of bouquets made

        for (int num : arr) {
            if (num <= day) {          // flower bloomed
                consecutive++;
                if (consecutive == k) { // enough for one bouquet
                    bouquets++;
                    consecutive = 0;    // reset for next
                    if (bouquets >= m) return true; // early stop
                }
            } else {
                consecutive = 0;        // break streak
            }
        }

        return bouquets >= m;
    }
}

```

