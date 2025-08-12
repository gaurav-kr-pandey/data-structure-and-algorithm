https://leetcode.com/problems/majority-element/description/

### Intuition:

**Approach 1: (Brute Force)**
Use two loops first $i \to n$ to keep track of each elements, second $j \to n$ that traverse whole array and count that element. Then we can keep updating maxCount element. This solution requires $O(n^2)$ Time Complexity.

**Approach 2: Frequency Map**
Maintain frequency of each element in the map by running single loop $i \to n$. This is a bit optimised in terms of Time Complexity $O(n)$ but requires extra space of $O(n)$

**Approach 3 : Moore's Voting Algorithm**

*Moore's Voting Algorithm* says that if there are multiple candidate in a election and if there exists a candidate who got vote(v)  $\to v > \frac{n}{2}$ times must cancel out rest of the candidate and still remains with count > 0.

Time Complexity: $O(n)$
Space Complexity: $O(1)$

**Code:**

```java
class Solution {
    public int majorityElement(int[] nums) {

        int count = 1;
        int ele = nums[0];
        int length = nums.length;

        for (int i = 1; i < length; i++) {
            if (nums[i] == ele) {
                count++;
            } else {
                count--;
                if (count == 0) {
                    ele = nums[i];
                    count = 1;
                }
            }
        }

        count = 0;
        for (int i : nums) {
            if (i == ele)
                count++;
        }

        return count > nums.length / 2 ? ele : 0;
    }
}
```