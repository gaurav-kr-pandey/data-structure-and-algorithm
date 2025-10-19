https://www.geeksforgeeks.org/problems/second-largest3735/1

## Code:

```java
class Solution {
    public int getSecondLargest(int[] arr) {
        int largest = Integer.MIN_VALUE;
        int secLargest = Integer.MIN_VALUE;

        for (int num : arr) {
            if (num > largest) {
                secLargest = largest;
                largest = num;
            } else if (num < largest && num > secLargest) {
                secLargest = num;
            }
        }

        return (secLargest == Integer.MIN_VALUE) ? -1 : secLargest;
    }
}


```