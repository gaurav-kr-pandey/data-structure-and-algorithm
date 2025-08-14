## **1. Concept**
- **Definition:**  
  A divide-and-conquer algorithm that efficiently finds an element or a boundary in a **sorted** array (or in any range where the property is monotonic).
- **Precondition:**  
  Array (or range) must be **sorted** or have a monotonic property.

---

## **2. Core Steps**
1. **Initialize boundaries:**

```plaintext
   low  = 0
   high = n - 1
```

2. **While** `low <= high`:
   - Compute `mid = low + (high - low) / 2` (avoid overflow)
   - Compare `arr[mid]` with target:
     - If `arr[mid] == target` → found
     - If `target < arr[mid]` → go left (`high = mid - 1`)
     - Else → go right (`low = mid + 1`)

---

## **3. Exact Element Search (Template)**
```java
public int binarySearch(int[] arr, int target) {
    int low = 0, high = arr.length - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] > target) {
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }
    return -1; // Not found
}
```

---

## **4. Variants**

### **Lower Bound** – First index where `arr[i] >= target`
```java
public int lowerBound(int[] arr, int target) {
    int low = 0, high = arr.length;
    while (low < high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] < target) {
            low = mid + 1;
        } else {
            high = mid;
        }
    }
    return low; // Could be arr.length if target > all elements
}
```

---

### **Upper Bound** – First index where `arr[i] > target`
```java
public int upperBound(int[] arr, int target) {
    int low = 0, high = arr.length;
    while (low < high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] <= target) {
            low = mid + 1;
        } else {
            high = mid;
        }
    }
    return low;
}
```

---

### **First Occurrence in Duplicates**
```java
public int firstOccurrence(int[] arr, int target) {
    int low = 0, high = arr.length - 1, ans = -1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == target) {
            ans = mid;
            high = mid - 1; // Keep searching left
        } else if (arr[mid] > target) {
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }
    return ans;
}
```

---

### **Last Occurrence in Duplicates**
```java
public int lastOccurrence(int[] arr, int target) {
    int low = 0, high = arr.length - 1, ans = -1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == target) {
            ans = mid;
            low = mid + 1; // Keep searching right
        } else if (arr[mid] > target) {
            high = mid - 1;
        } else {
            low = mid + 1;
        }
    }
    return ans;
}
```

---

## **5. Complexity**
- **Time:** `O(log n)`
- **Space:** `O(1)`

---

## **6. When to Use Normal Binary Search**
- Array is **sorted** (ascending or descending).
- The decision to go left or right is based on a direct **comparison** with the mid value.
- You are looking for:
  - An exact value
  - A boundary index (first/last occurrence, lower/upper bound)

---

## **7. Pitfalls**
- Forgetting to use `low + (high - low) / 2` to avoid overflow.
- Infinite loops due to incorrect `low`/`high` updates.
- Confusing lower bound and upper bound logic.
- Not handling duplicates when needed.

---

## **8. Common Problem Patterns**
| Problem Type              | Example                                     |
|---------------------------|---------------------------------------------|
| Exact Search              | Find a number in sorted array               |
| Boundary Search           | Lower Bound / Upper Bound                   |
| First/Last Occurrence     | Count frequency of element in sorted array  |
| Rotated Sorted Array      | Search with extra rotation checks           |
| Peak Finding              | Find local maximum in an array              |

---

## **9. Visual Flow**
```plaintext
low = 0, high = n - 1
       ↓
while low <= high:
    mid = low + (high - low) / 2
    if arr[mid] == target → return mid
    if arr[mid] > target → high = mid - 1
    else → low = mid + 1
return -1
```
