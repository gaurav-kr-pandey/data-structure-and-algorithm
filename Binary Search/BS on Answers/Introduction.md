
# **Binary Search on Answer Space – Reference Notes**

## **1. Concept**
- **Normal Binary Search:**  
    Operates on an array (or list) directly to find an element or boundary.

- **Binary Search on Answer Space:**  
    Operates on the **range of possible answers**, not the array itself.  
    Used when:
    1. The answer is **monotonic** in some way — if a certain value is valid, all smaller (or larger) values are also valid or invalid.
    2. You can **check** whether a candidate answer is valid via a helper function in `O(f(...))`.

---

## **2. Core Steps**
1. **Identify the search space**:
    - Minimum possible answer → `low`
    - Maximum possible answer → `high`

2. **Write a predicate function `can(mid)`**:  
    Returns `true` if the candidate `mid` is a valid answer.

3. **Apply Binary Search on this space**:
    - If `can(mid)` is `true` → we can try smaller/better answers (`high = mid - 1` if minimizing).
    - If `can(mid)` is `false` → we must try bigger/worse answers (`low = mid + 1` if minimizing).

4. **Return the final valid answer**.
---

## **3. Template (Minimize Answer)**

```java
public int binarySearchAnswer(int low, int high) {
    int ans = -1; // or appropriate default
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (can(mid)) {
            ans = mid;
            high = mid - 1; // try smaller value
        } else {
            low = mid + 1; // try larger value
        }
    }
    return ans;
}

private boolean can(int mid) {
    // Implement feasibility check
    return true;
}

```

**For Maximizing Answer**:  
Reverse the movement:
- If `can(mid)` → try larger (`low = mid + 1`)
- Else → smaller (`high = mid - 1`)

---
## **4. Key Observations**
- Works best when the **feasibility check** is cheaper than iterating over the entire space blindly.
- **Search space doesn’t have to be array elements** — can be integers, doubles, even conceptual values like time, speed, capacity.
- If the space is over `long` range, careful with overflow in `mid` calculation.

## **5. Common Problems & Patterns**

| Problem                                            | Search Space                       | Predicate (`can(mid)`) meaning                             |
| -------------------------------------------------- | ---------------------------------- | ---------------------------------------------------------- |
| **Aggressive Cows**                                | Distance between cows              | Can we place cows at least `mid` distance apart?           |
| **Painter Partition**                              | Max load (time)                    | Can we paint within `mid` time using given painters?       |
| **Capacity to Ship Packages in D Days**            | Ship capacity                      | Can we ship in D days with capacity `mid`?                 |
| **Koko Eating Bananas**                            | Eating speed                       | Can Koko eat all bananas in `h` hours at speed `mid`?      |
| **Minimize Maximum Distance Between Gas Stations** | Distance between stations (double) | Can we add ≤ k stations to keep distance ≤ mid?            |
| **Allocate Books**                                 | Pages per student                  | Can we assign books so that no student gets > `mid` pages? |

## **6. When to Think “Answer Space” Binary Search**
Ask:
1. Is the answer numeric and bounded within `[low, high]`?
2. Can I check if a candidate is valid in a deterministic way?
3. Is the validity monotonic?
    - If `mid` works, all bigger (or smaller) should also work.

If YES → likely an answer space binary search.

---

## **7. Complexity**
- Let:
    - `N` = size of input data
    - `check()` = complexity of predicate function
    - `S` = size of search space (usually `high - low + 1`)

**Time:** `O(log S * check())`  
**Space:** depends on `check()`, usually `O(1)`.

---

## **8. Pitfalls**

- **Wrong monotonicity assumption** → binary search won't work.
- **Off-by-one** in `low`/`high` updates → infinite loop.
- Not handling the final return correctly → sometimes last valid `mid` is lost if `ans` not stored.
- Forgetting that `low` and `high` can be outside array bounds.

---

## **9. Variants**

- **Floating Point Answer Space**:  
    Repeat binary search for fixed number of iterations (precision limit).

```java
double eps = 1e-6;
while (high - low > eps) {
    double mid = (low + high) / 2.0;
    if (can(mid)) {
        ans = mid;
        high = mid; 
    } else {
        low = mid;
    }
}

```

**Multi-dimensional Search Space**:  
Rare, but can be reduced to 1D in some problems.

## **10. Quick Checklist Before Coding**

✅ Identify low & high  
✅ Ensure monotonicity of `can()`  
✅ Decide if minimizing or maximizing  
✅ Write `can()` clearly  
✅ Avoid overflow in mid  
✅ Store `ans` when needed

---

## **Binary Search on Answer Space – Flow Diagram**

```vbnet
          ┌────────────────────────────────┐
          │ 1. Identify Search Space        │
          │   low = min possible answer     │
          │   high = max possible answer    │
          └────────────────────────────────┘
                          │
                          ▼
          ┌────────────────────────────────┐
          │ 2. Define Predicate can(mid)    │
          │   returns TRUE if candidate     │
          │   'mid' is a feasible answer.   │
          │   (must be monotonic)           │
          └────────────────────────────────┘
                          │
                          ▼
          ┌────────────────────────────────┐
          │ 3. While low <= high            │
          └────────────────────────────────┘
                          │
                          ▼
          ┌────────────────────────────────┐
          │ mid = low + (high - low) / 2    │
          └────────────────────────────────┘
                          │
              ┌───────────┴────────────┐
              ▼                        ▼
   ┌───────────────────────┐  ┌─────────────────────────┐
   │ if can(mid) == true    │  │ if can(mid) == false    │
   └───────────────────────┘  └─────────────────────────┘
              │                        │
  Minimizing: │ high = mid - 1         │ low = mid + 1
  Maximizing: │ low = mid + 1          │ high = mid - 1
              │                        │
              ▼                        ▼
          Store ans = mid   (if needed for min/max)
                          │
                          ▼
          ┌────────────────────────────────┐
          │ 4. Return final stored ans      │
          │    (or low/high depending)      │
          └────────────────────────────────┘

```

### **Quick Visual for Monotonicity Check**

- **Minimizing:**
```pgsql
       Feasible Zone
<----------------------✓✓✓✓✓ | ✗✗✗✗✗------------------>
low                             high
```

- **Maximizing:**
```pgsql
       Feasible Zone
<----------------------✗✗✗✗✗ | ✓✓✓✓✓------------------>
low                             high
```

### **Mini Example – Aggressive Cows**

1. **Search Space:**  
    low = 1, high = max(stall) - min(stall)
2. **can(mid):**  
    Can we place cows with at least `mid` distance apart?
3. **Monotonicity:**  
    If `mid` works, all smaller distances also work → **Maximizing** type.
