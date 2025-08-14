Koko loves to eat bananas. There are `n` piles of bananas, the `ith` pile has `piles[i]` bananas. The guards have gone and will come back in `h` hours.
Koko can decide her bananas-per-hour eating speed of `k`. Each hour, she chooses some pile of bananas and eats `k` bananas from that pile. If the pile has less than `k` bananas, she eats all of them instead and will not eat any more bananas during this hour.
Koko likes to eat slowly but still wants to finish eating all the bananas before the guards return.
Return _the minimum integer_ `k` _such that she can eat all the bananas within_ `h` _hours_.

[Leetcode - Practice](https://leetcode.com/problems/koko-eating-bananas/)
## Intuition:

**Observations:**
- `piles[i]` _$\to$ piles of Bananas at ith pile_
- `n` $\to$ _total piles_
- `h`  $\to$ _eat all bananas with in h hours_ (*Note* : she can take less than or equals to h hours)
- `k` $\to$ per hour eating speed `k/hour`
- Return _the minimum integer_ `k` _such that she can eat all the bananas within_ `h` _hours_

**What is the minimum possible value of `k` such that Koko can eat all bananas in `h` hours ?**
Minimum banana can not be less than `1 banana/hour` 

```java
minimum = low = 1
```

**What is the maximum possible value of `k` such that Koko can eat all banana's in `h` hours ?**
Maximum banana that Koko can eat in 1 hour is max(piles) = maximum bananas in one piles

```java
maximum = high = max(piles)
```

now, my answer `k` lies from $min \to max$, because we need minimum integer `k` _such that she can eat all the bananas within_ `h` _hours_.

**Approach 1:**
start from $min \to max$ and try all possible value of `k`

_If n = length of array, and m = max value of array _
- _Time Complexity:_ $O(n * m)$ 
- _Space Complexity:_ $O(1)$

**Approach 2:**
If we look closely we have a $min = 1$ and a $max  = max(array)$, that can be a answer space for a binary search algorithm and we can reduce the time complexity of linearly traversing from $(min = 1) \to max$  to logarithmic($log_2 m$) time complexity.
_If n = length of array, and m = max value of array _
- _Time Complexity:_ $O(n log m)$ 
- _Space Complexity:_ $O(1)$

Here, minimum k can be 1 and maximum k can be max(piles)
So, answer space for BS is low = 1, high = max(piles)

**Do we need to sort the array?**
No, order of eating all the bananas does not matter, Koko should finish all the bananas in any order within `h` hours.

This code here checks number of hours required to eat current piles -

```java
int pile = piles[i];
hour -= (pile/k); // subtract total hours to eat current pile 
if (pile % k != 0) {
    hours = hours - 1; // subtract 1 if we have remainder(banana) left (less than k)
}
```

or we can optimise this even further as - 
```java 
hour -= (pile + k - 1) / k;
```

So, we will keep shrinking our mid to lower value if we can eat all bananas from current mid and will expand it if, he can not eat.

### Code:

```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        int n = piles.length, low = 1, k = 1;
        int high = Arrays.stream(piles).max().getAsInt();

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (canEatAll(piles, h, mid)) {
                k = mid;
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return k;
    }

    private boolean canEatAll(int[] piles, int h, int k) {
        int j = 0, n = piles.length;

        for (int i = 0; i < n; i++) {
            int curr = piles[i];
            h = h - (curr / k); // subtract total hours to eat current pile

            if (curr % k != 0) {
                h--; // subtract 1 if we have remainder(banana) left (less than k)
            }
        }

        return h >= 0; // Koko can eat all bananas within or eq to h hours
    }
}
```