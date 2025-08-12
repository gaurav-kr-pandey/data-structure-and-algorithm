https://leetcode.com/problems/next-permutation/description/

### Solution

**Algorithm:**

1. Find first element `x` that is `nums[i - 1] < nums[i]` $\to$  from end ($n \to 0$)
2. Find first element that is greater `x` (in step1) $\to$  from end ($n \to 0$)
3. Swap`index1, index2`
4. Reverse/Sort the array after `index1`

**Code:**

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int index1 = -1;
        int index2 = -1;
        
        //Step-1: Find first element x that is nums[i - 1] < nums[i] <-- from end (n - 1 --> 0)
        // x = nums[i - 1]
        for(int i = nums.length - 1; i > 0; i--){
            if(nums[i - 1] < nums[i]){
                index1 = i - 1;
                break;
            }
        }
        
        // Edge Case : If the number is greatest possible, just reverse 
        if(index1 == -1){
            reverse(nums, 0);
            return;
        }
        
        //Step-2: Find first element that is greater x=nums[index1] (in step1) - from end 
        for(int i = nums.length - 1; i >= 0; i--){
            if(nums[index1] < nums[i]){
                index2 = i;
                break;
            }
        }
        
        //Step-3: Swap index1, index2
        swap(nums, index1, index2);
        //Step-4: Reverse/Sort the array after index1
        reverse(nums, index1 + 1);
    }
    
    void swap(int[] nums, int i, int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    
    void reverse(int[] nums, int start){
        int i = start, j = nums.length - 1;
        
        while(i <= j){
            swap(nums, i, j);
            i++; 
            j--;
        }
    }
}

```