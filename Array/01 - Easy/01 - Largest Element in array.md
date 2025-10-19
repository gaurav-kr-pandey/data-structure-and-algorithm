https://www.geeksforgeeks.org/problems/largest-element-in-array4009/1

## Code :

```java
class Solution {
    public static int largest(int[] arr) {
        int max = Integer.MIN_VALUE;
    
        for (int x : arr) {
            max = Math.max(max, x);
        }
    
        return max;
    }
}

```