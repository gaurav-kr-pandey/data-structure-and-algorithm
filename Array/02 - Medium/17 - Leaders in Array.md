
https://www.geeksforgeeks.org/problems/leaders-in-an-array-1587115620/1

You are given an array **`arr`** of positive integers. Your task is to find all the leaders in the array. An element is considered a leader if it is greater than or equal to all elements to its right. The rightmost element is always a leader.

**Examples:  
**Input:** arr = [16, 17, 4, 3, 5, 2]
**Output:** [17, 5, 2]
**Explanation:** Note that there is nothing greater on the right side of 17, 5 and, 2.

## Code

```java

class Solution {
    static ArrayList<Integer> leaders(int arr[], int n) {
    
        int max = Integer.MIN_VALUE;
        ArrayList<Integer> leaders = new ArrayList<>();
        
        for(int i = n - 1; i >- 1; i--) {
            if(max <= arr[i]) {
                leaders.add(arr[i]);
            }
            max = Math.max(max,arr[i]);
        }
        
        Collections.reverse(leaders);
        
        return leaders;
         
    }
}
```