https://leetcode.com/problems/merge-sorted-array/description/

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        
        int i = m - 1;
        int j = n - 1;
        int k = n + m - 1;

        while (j >= 0 && i >= 0) {
            if (nums1[i] < nums2[j]) {
                nums1[k--] = nums2[j--];
            } else {
                nums1[k--] = nums1[i--];
            }
        }

        while (i >= 0)
            nums1[k--] = nums1[i--];

        while (j >= 0)
            nums1[k--] = nums2[j--];
    }
}
```

