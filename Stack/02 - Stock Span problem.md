https://www.geeksforgeeks.org/problems/stock-span-problem-1587115621/1

The stock span problem is a financial problem where we have a series of daily price quotes for a stock and we need to calculate the span of stock price for all days. The span **`arr[i]`** of the stocks price on a given day **i** is defined as the maximum number of consecutive days just before the given day, for which the price of the stock on the given day is less than or equal to its price on the current day.

**Input**: `arr[]` = `[100, 80, 60, 70, 60, 75, 85]`
**Output**: `[1, 1, 1, 2, 1, 4, 6]`

Reference: [[01 - Next Greater Element to Right]]
### Intuition:

This problem is exactly same as Finding `Next Greater Element to Left`
It is just that we need to maintain `index` in the monotonic increasing($top \to bottom$)
so that we can find the consecutive days.
### Code:

```java
class Solution {
    public List<Integer> calculateSpan(int[] arr) {
        
        List<Integer> list = new ArrayList<>();
        Deque<Integer> stack = new ArrayDeque<>();
        
        for (int i = 0; i < arr.length; i++) {
            while (!stack.isEmpty() && arr[stack.peek()] <= arr[i]) {
                stack.pop();
            }
            
            int ngIndex = stack.isEmpty() ? - 1 : stack.peek();
            list.add(i - ngIndex);
            
            stack.push(i);
        }
        
        return list;
    }
}
```