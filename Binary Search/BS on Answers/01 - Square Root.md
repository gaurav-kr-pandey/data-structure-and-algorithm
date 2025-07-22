[GFG - Practice](https://www.geeksforgeeks.org/problems/square-root/1)

```java
class Solution {
    int floorSqrt(int n) {
        int low = 1, high = n, sqrt = n / 2;
        
        while (low <= high) {
            int mid = low + (high - low) / 2;
            
            if (mid * mid == n) {
                return mid;
            }
            

            if (mid * mid < n) {
                sqrt = mid;
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        
        return sqrt;
    }
}
```