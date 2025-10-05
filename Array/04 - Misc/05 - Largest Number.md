https://leetcode.com/problems/largest-number/description/

Given a list of non-negative integers `nums`, arrange them such that they form the largest number and return it.
Since the result may be very large, so you need to return a string instead of an integer.

### Intuition:
We can think of something like converting `int[]` to `string[]` and sort it by using `Arrays.sort(arr)`. Then append it using `StringBuilder`.

**_Catch:_ Normal sorting will not work.**
`[3, 30, 34` will be sorted as $\to$ `[34,30, 3]` but expectation is `3` should come before `30` then it will produce largest number `34330`

#### Why can't we use `Arrays.sort(arr)` directly?

- If used `Arrays.sort(arr)` which sorts strings in normal lexicographic order.
	- Example: `[3,30,34]` becomes `"30","3","34"` → `"34330"` which is wrong.
- The correct rule is: for two numbers `a` and `b`, compare `"ab"` vs `"ba"`.
    - Keep the order that produces the larger concatenation.
- You can directly convert `nums` to a `String[]` and sort with a comparator.
### Code:

```java
class Solution {
    public String largestNumber(int[] nums) {
        String[] arr = new String[nums.length];
        for (int i = 0; i < nums.length; i++) {
            arr[i] = String.valueOf(nums[i]);
        }

		// "3" + "1" or "1" + "3"
        Arrays.sort(arr, (a, b) -> (b + a).compareTo(a + b));

        if (arr[0].equals("0")) return "0"; // all zeros case

        StringBuilder sb = new StringBuilder();
        for (String s : arr) {
            sb.append(s);
        }
        return sb.toString();
    }
}
```

### Complexity

- **Time**: $O(n log n * k)$ (n = numbers, k = average string length, sorting dominates).
- **Space**: $O(n * k)$ (strings storage).