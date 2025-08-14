
```java

class Solution {

    public int solve(int n, int k, int[] stalls) {
        Arrays.sort(stalls);
        int low = 1, high = stalls[n - 1] - stalls[0] + 1, min = 1;
        while (low <= high) {
            int mid = (low + high) / 2;

            if (isPossible(stalls, k, mid)) {
                min = mid;
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return min;
    }

    public boolean isPossible(int[] stalls, int k, int d) {
        int i = 0, j = 1, x = 1, n = stalls;
        int maxStalls = stalls[j] - stalls[i];
        while (j < n) {
            if (maxStalls >= d) {
                x++;
                i = j;
            }
            if (x == k) break;
            j++;
        }
        return k == x;
    }
}

```