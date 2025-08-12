https://leetcode.com/problems/majority-element-ii/

Given an integer array of size `n`, find all elements that appear more than `⌊ n/3 ⌋` times.

**Example 1:**
**Input:** nums = [3,2,3]
**Output:** [3]

## Solution 

**Moore's Voting Algorithm** :


```java
class Solution {
    public List<Integer> majorityElement(int[] nums) {
    
        int n = nums.length; 
        int candidate1 = 0, count1 = 0;
        int candidate2 = 0, count2 = 0;
        List<Integer> list = new ArrayList<>();


        for (int ele : nums) {
            if (ele == candidate1) {
                count1++;
            } else if (ele == candidate2) {
                count2++;
            } else if (count1 == 0) {
                candidate1 = ele;
                count1 = 1;
            } else if (count2 == 0) {
                candidate2 = ele;
                count2 = 1;
            } else {
                count1--;
                count2--;
            }
        }

        count1 = 0; 
        count2 = 0;

        for (int ele : nums) {
            if (candidate1 == ele) {
                count1++;
            } else if (candidate2 == ele) {
                count2++;
            }
        }

        if (count1 > n / 3) list.add(candidate1);
        if (count2 > n / 3) list.add(candidate2);

        return list;
    }
}
```