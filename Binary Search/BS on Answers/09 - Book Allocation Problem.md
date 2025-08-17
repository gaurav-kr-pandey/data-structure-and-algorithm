https://www.geeksforgeeks.org/problems/allocate-minimum-number-of-pages0937/1

**Problem Explanation:**
`arr[] of integers`  - books
`arr[i]` - number of pages in current book
`k` - number of students

**Goal:**
Allocate books to each students such that:
- Each student receives atleast one book.
- Each student is assigned a contiguous sequence of books.
- No book is assigned to more than one student.

The objective is to **minimize the maximum number of pages** assigned to any student. In other words, out of all possible allocations, find the arrangement where the student who receives the most pages still has the **smallest possible maximum**.

**Note:** If it is not possible to allocate books to all students, return **-1**.

**Examples:**
**Input:** `arr[] = [12, 34, 67, 90]`, k = 2
**Output:** 113
**Explanation:** Allocation can be done in following ways:  
=> `[12]` and `[34, 67, 90]` Maximum Pages = 191  
=> `[12, 34]` and `[67, 90]` Maximum Pages = 157  
=> `[12, 34, 67]` and `[90]` Maximum Pages = 113.  
The third combination has the minimum pages assigned to a student which is 113.

### Intuition:

**What is the maximum number of pages we can assign to any student?**
If we assign all the books to one student then it will be maximum number that can be assigned to one student. 

`high = sum(arr)`

**What is the minimum number of pages we can assign to any student?**
- Think about the **biggest single book**.
- That book **must go to some student**, no matter how we divide them.
- So the minimum possible maximum pages must be **at least that book’s size**.
- If we set `low` smaller than `max(arr)`, it’s pointless, because we’d never be able to allocate that largest book within that bound (We do not largest book to be clubbed with any other book because distribution needs to such that we need to **minimize the maximum number of pages**).

`low = min(arr)`

**Code:**

```java
class Solution {
    public int findPages(int[] arr, int k) {
        int low = Arrays.stream(arr).max().getAsInt();
        int high = Arrays.stream(arr).sum();
        int n = arr.length, pages = low;
        if (arr.length < k) return -1; // or handle as per problem definition

        while (low <= high) {
            int mid = low + (high - low) / 2;
            
            if (canAllocate(arr, k, mid)) {
                high = mid - 1;
                pages = mid;
            } else {
                low = mid + 1;
            }
        }
        
        return pages;
    }
    
    private boolean canAllocate(int[] arr, int k, int mid) {
        int curr = 0, n = arr.length;
        int std = 1; // add pages for student-1 till mid
        
        for (int i = 0; i < n; i++) {
            if (curr + arr[i] > mid) { // If it exceeds mid we will not add and start adding for student-2
                std++;
                curr = arr[i];
            } else {
	            // Keep adding for current student
                curr += arr[i];
            }
            if (std > k) { // if we are able to distribute pages more than k students then distribution is not correct
                return false;
            }
        }
        
        return true;
    }
}
```