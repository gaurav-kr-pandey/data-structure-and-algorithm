https://leetcode.com/problems/fruit-into-baskets/description/

### Solution:

This problem is same - [[03 - Longest Substring with k unique characters]] , Pick Toys


```java
class Solution {

    public int totalFruit(int[] fruits) {
        int i = 0, j = 0, n = fruits.length, maxFruits = 0;
        Map<Integer, Integer> seen = new HashMap<>();
        while (j < n) {
            seen.put(fruits[j], seen.getOrDefault(fruits[j], 0) + 1);
            while (seen.size() > 2) {
                seen.put(fruits[i], seen.get(fruits[i]) - 1);
                if (seen.get(fruits[i]) == 0) {
                    seen.remove(fruits[i]);
                }
                i++;
            }
            maxFruits = Math.max(maxFruits, j - i + 1);
            j++;
        }
        return maxFruits;
    }
}

```