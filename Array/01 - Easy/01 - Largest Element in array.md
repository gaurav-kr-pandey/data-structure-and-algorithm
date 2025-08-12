
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