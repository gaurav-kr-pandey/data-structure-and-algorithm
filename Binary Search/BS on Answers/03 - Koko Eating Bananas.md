[Leetcode - Practice](https://leetcode.com/problems/koko-eating-bananas/)

## Solution:

Here, minimum k can be 1 and maximum k can be max(piles)
So, answer space for BS is low = 1, high = max(piles)
This code here checks number of hours required to eat current piles -
```java
			int pile = piles[i];
            totalHours += pile/k;
            if (pile % k != 0) {
                totalHours++;
            }
```

or we can optimise this even further as - 
```java 
	totalHours += (pile + k - 1) / k;
```
So, we will keep shrinking our mid to lower value if we can eat all bananas from current mid and will expand if can not eat.

### CODE:
```java
class Solution {
    public int minEatingSpeed(int[] piles, int h) {
        int max = piles[0];
        int k = 1;
        for (int curr : piles) {
            max  = Math.max(max, curr);
        }

        int low = 1, high = max, ans = 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (canEatAll(piles, h, mid)) {
                ans = mid;
                high = mid - 1;
            } else {
                low = mid + 1;
            }
        }

        return ans;
    }

    private boolean canEatAll(int[] piles, int h, int k) {
        int totalHours = 0;
        for (int i = 0; i < piles.length; i++) {
            int pile = piles[i];
            totalHours += pile/k;
            if (pile % k != 0) {
                totalHours++;
            }

            if (totalHours > h) {
                return false;
            }
        }

        return true;
    }
}
```