https://www.geeksforgeeks.org/problems/maximum-rectangular-area-in-a-histogram-1587115620/1

You are given a **histogram** represented by an array **arr**, where each element of the array denotes the **height** of the bars in the histogram. All bars have the same **width of 1 unit**.
Your task is to find the **largest** rectangular area possible in the given histogram, where the rectangle can be formed using a number of contiguous bars.

**Input:** `arr[] = [60, 20, 50, 40, 10, 50, 60]`
 
![Largest-Rectangular-Area-in-a-Histogram](https://media.geeksforgeeks.org/wp-content/uploads/20240924161857/Largest-Rectangular-Area-in-a-Histogram.webp)

**Output:** 100
**Explanation:** We get the maximum by picking bars highlighted above in green (50, and 60). The area is computed (smallest height) * (no. of the picked bars) = 50 * 2 = 100.

### Intuition:

**How to calculate histogram for every index `arr[i]` ?**
For example above - 
`arr[] = [60, 20, 50, 40, 10, 50, 60]`
`index = [00, 01, 02, 03, 04, 05, 06]`

Let's look for index `3` , 
`index3` -  `((4 - 1) - 1) * arr[3]`, where 
	`4 ` - index of next greater element to right
	`1 ` - index of next greater element to left
	`-1` - We need histogram `40, 50` with length `2` but `4 - 1` is giving `3` hence we need to decrement it by `-1`.

So, formula derived is:
```java
area(i) => 
([index of next greater to right] - [index of next greater to left] - 1) * arr[i]
```

**What if there is no greater element to left/right?**
To satisfy the formula, we need these two value, hence if we do not have either of them we will take following values as default option:
```lisp
	ngeIndex left  --> -1
	ngeIndex right --> arr.length + 1
```

