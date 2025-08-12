https://www.geeksforgeeks.org/problems/inversion-of-array-1587115620/1

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