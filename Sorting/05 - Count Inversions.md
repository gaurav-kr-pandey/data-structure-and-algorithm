### Count Inversions

Given an array of integers **arr[]**. Find the **Inversion Count** in the array.  
Two elements arr[i] and arr[j] form an inversion if **arr[i] > arr[j]** and **i < j**.

> _**Inversion Count**:_ For an array, inversion count indicates how far (or close) the array is from being sorted. If the array is already sorted then the inversion count is 0.  
> If an array is sorted in the reverse order then the inversion count is the maximum. 

**Examples:**

**Input**: arr[] = [2, 4, 1, 3, 5]  
**Output**: 3
**Explanation**: The sequence 2, 4, 1, 3, 5 has three inversions (2, 1), (4, 1), (4, 3).

**Input**: arr[] = [2, 3, 4, 5, 6]  
**Output**: 0
**Explanation**: As the sequence is already sorted so there is no inversion count.

**Input**: arr[] = [10, 10, 10]  
**Output**: 0
**Explanation**: As all the elements of array are same, so there is no inversion count.

**Constraints:**  
1 ≤ arr.size() ≤ 105  
1 ≤ arr[i] ≤ 104

## Solution

Count inversion

```java
class Solution {
    static int count = 0;
    static int inversionCount(int arr[]) {
        count = 0;
        mergeSort(arr, 0, arr.length - 1);
        return count;
    }
    
    static void mergeSort(int[] arr, int left, int right) {
        if (left < right) {
            int mid = left + (right - left) / 2;
            mergeSort(arr, left, mid);
            mergeSort(arr, mid + 1, right);
            merge(arr, left, mid, right);
        }
    }
    
    static void merge(int[] arr, int left, int mid, int right) {
        int n = mid - left + 1;
        int m = right - mid;
        int[] arr1 = new int[n];
        int[] arr2 = new int[m];
        
        for (int i = 0; i < n; i++) {
            arr1[i] = arr[left + i];
        }
        
        for (int j = 0; j < m; j++) {
            arr2[j] = arr[mid + 1 + j];
        }
        
        int i = 0, j = 0, k = left;
        
        while (i < n && j < m) {
            if (arr1[i] <= arr2[j]) {
                arr[k++] = arr1[i++];
            } else {
                arr[k++] = arr2[j++];
                
                /**
                 * If arr1[i] > arr2[j]
                 * It means all the element in the arr1 from i --> n 
                 * will be greater than arr2[j], 
                 * hence, we add (n - i) in inversion count
                 * **/
                count = count + (n - i);
            }
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