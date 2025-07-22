

```java
class Solution {

    int count = 0;

    public int reversePairs(int[] nums) {
        mergeSort(nums, 0, nums.length - 1);
        return count;
    }

    void mergeSort(int[] nums, int left, int right) {
        if (left < right) {
            int mid = (left + right) / 2;
            mergeSort(nums, left, mid);
            mergeSort(nums, mid + 1, right);
            merge(nums, left, mid, right);
        }
    }

    void merge(int[] nums, int left, int mid, int right) {

        // Count reverse pairs before merge
        int j = mid + 1;
        for (int i = left; i <= mid; i++) {
            while (j <= right && (long)nums[i] > 2L * nums[j]) {
                j++;
            }
            count += (j - (mid + 1));
        }


        int[] arr1 = new int[mid - left + 1];
        int[] arr2 = new int[right - mid];
        int n = arr1.length;
        int m = arr2.length;

        for (int i = 0; i < n; i++) {
            arr1[i] = nums[i + left];
        }

        for (int i = 0; i < m; i++) {
            arr2[i] = nums[i + mid + 1];
        }

        int i = 0, k = left;
        j = 0;
        
        while (i < n && j < m) {
            if (arr1[i] <= arr2[j]) {
                nums[k++] = arr1[i++];
            } else {
                nums[k++] = arr2[j++];
            }
        }

        while (i < n)
            nums[k++] = arr1[i++];

        while (j < m)
            nums[k++] = arr2[j++];
    }
}
```