[Leetcode - Practice](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)

```java
class Solution {
    public int search(int[] nums, int target) {
        int min = findMin(nums);

        if(min == 0) {
            return binarySearch(nums, target, 0, nums.length-1);
        }
        
        if(target >= nums[min] && target <= nums[nums.length-1]) {
            return binarySearch(nums, target, min, nums.length-1);
        } else {
            return binarySearch(nums, target, 0, min);
        }
    }

    private int binarySearch(int[] nums, int target, int low, int high) {
    
        while (low <= high) {
            int mid = (low + high) / 2;

            if (nums[mid] == target) {
                return mid;
            }
            
            if (nums[mid] < target) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }

        return -1;
    }

    public int findMin(int[] nums) {
        int low = 0, high = nums.length - 1, min = nums.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] > nums[high]) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }

			if (nums[mid] < nums[min]) {
				min = mid;
			}
			
        }

        return min;
    }
}
```

## One pass solution

```java
class Solution {
    public int search(int[] nums, int target) {
        int low = 0, high = nums.length - 1;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            if (nums[mid] == target) {
                return mid;
            }

			// Left half is sorted
            if (nums[low] <= nums[mid]) {
                if (target >= nums[low] && target <= nums[mid]) {
                    high = mid - 1;
                } else {
                    low = mid + 1;
                }
            } else {
            // Right half is sorted
                if (target >= nums[mid] && target <= nums[high]) {
                    low = mid + 1;
                } else {
                    high = mid - 1;
                }
            }
        }

        return -1;
    }
}
```