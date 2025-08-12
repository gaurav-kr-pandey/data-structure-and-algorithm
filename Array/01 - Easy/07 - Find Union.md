

```java
import java.util.*;

public class UnionSortedArrays {

    public static List<Integer> findUnion(int[] arr1, int[] arr2) {
        int n = arr1.length, m = arr2.length;
        int i = 0, j = 0;
        List<Integer> union = new ArrayList<>();

        while (i < n && j < m) {
            // Skip duplicates in arr1
            while (i > 0 && i < n && arr1[i] == arr1[i - 1]) i++;
            // Skip duplicates in arr2
            while (j > 0 && j < m && arr2[j] == arr2[j - 1]) j++;

            if (i < n && j < m) {
                if (arr1[i] < arr2[j]) {
                    union.add(arr1[i++]);
                } else if (arr2[j] < arr1[i]) {
                    union.add(arr2[j++]);
                } else {
                    // Same element, add only once
                    union.add(arr1[i]);
                    i++;
                    j++;
                }
            }
        }

        // Remaining elements of arr1
        while (i < n) {
            if (i == 0 || arr1[i] != arr1[i - 1]) {
                union.add(arr1[i]);
            }
            i++;
        }

        // Remaining elements of arr2
        while (j < m) {
            if (j == 0 || arr2[j] != arr2[j - 1]) {
                union.add(arr2[j]);
            }
            j++;
        }

        return union;
    }

    public static void main(String[] args) {
        int[] arr1 = {1, 2, 2, 3, 4};
        int[] arr2 = {2, 3, 5, 6};

        List<Integer> result = findUnion(arr1, arr2);
        System.out.println("Union: " + result);
    }
}

```