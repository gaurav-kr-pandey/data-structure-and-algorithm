
**Merge Sort** is a popular **Divide and Conquer** algorithm used for sorting. It divides the array into smaller subarrays, sorts them, and then merges them back into a single sorted array.

---
### Key Concepts:

1. **Divide**: Split the array into two halves recursively until each subarray has only one element.
2. **Conquer**: Recursively sort the subarrays.
3. **Merge**: Merge the sorted subarrays into a larger sorted array.

---
### Time and Space Complexity

|Complexity|Value|
|---|---|
|Time|O(n log n)|
|Space|O(n) (for temp array)|
|Stable|Yes|
|In-place|No (needs extra space)|

---

### Step-by-Step Explanation (with Example)

#### Example: 
`arr = [38, 27, 43, 3, 9, 82, 10]`

1. **Divide**:
    `[38, 27, 43, 3, 9, 82, 10] => [38, 27, 43] and [3, 9, 82, 10] => [38], [27, 43] and [3, 9], [82, 10] => ...`
    
2. **Sort and Merge**:
    `[27, 43] => merge -> [27, 43] [38], [27, 43] => merge -> [27, 38, 43] ...`


```java
package sorting;  
  
public class MergeSort {  
  
    public static void main(String[] args) {  
        int[] arr = ArrayUtil.generateRandomArray(20);  
        ArrayUtil.print(arr);  
        MergeSort mergeSort = new MergeSort();  
        mergeSort.sort(arr, 0, arr.length - 1);  
        ArrayUtil.print(arr);  
        ArrayUtil.isSorted(arr);  
    }  
  
  
    private void sort(int[] arr, int left, int right) {  
  
        if (left < right) {  
            int mid = (left + right) / 2;  
            sort(arr, left, mid);  
            sort(arr, mid + 1, right);  
            merge(arr, left, mid, right);  
        }  
  
    }  
  
    private void merge(int[] arr, int left, int mid, int right) {  
  
        int[] arr1 = new int[mid - left + 1];  
        int[] arr2 = new int[right - mid];  
        int n = arr1.length;  
        int m = arr2.length;  
  
        int i = 0, j = 0;  
  
        for (int x = left; x <= mid; x++) {  
            arr1[i++] = arr[x];  
        }  
  
        for (int x = mid + 1; x <= right; x++) {  
            arr2[j++] = arr[x];  
        }  
  
        i = 0;  
        j = 0;  
        int k = left;  
  
        while (i < n && j < m) {  
            if (arr1[i] <= arr2[j]) {  
                arr[k] = arr1[i];  
                i++;  
            } else {  
                arr[k] = arr2[j];  
                j++;  
            }  
            k++;  
        }  
  
        while (i < n) {  
            arr[k++] = arr1[i++];  
        }  
  
        while (j < m) {  
            arr[k++] = arr2[j++];  
        }  
  
    }  
  
}

```


### Explanation of Key Methods

#### `sort(arr, left, right)`
- Recursively splits the array into halves
- Calls `merge` to combine the sorted halves.

#### `merge(arr, left, mid, right)`
- Creates temporary arrays for left and right halves.
- Compares elements from both arrays and copies the smaller one into the original array.
- Copies remaining elements after the main comparison loop.

---

### When to Use Merge Sort?

- When **stable sort** is required.
- When working with **linked lists** (merge sort can be done in O(1) space for linked lists).
- When performance is more important than memory usage.