
### ✅ 1. **Matrix Multiplication Basics**

- Understand how matrix multiplication works:
    
    - A matrix of size `A x B` multiplied by `B x C` gives a matrix of size `A x C`.
        
    - Cost = `A * B * C` scalar multiplications.
        

---

### ✅ 2. **Associativity of Multiplication**

- Matrix multiplication is **associative**, not commutative:
    
    - `(A * B) * C ≠ A * (B * C)`
        
    - But both give the same final result, just **different costs**.
        
- This is why the **order of multiplication matters** in MCM.
    

---

### ✅ 3. **Problem Statement of MCM**

Given an array `arr[]` of length `n`, where the dimensions of matrices are:

- `Matrix1 = arr[0] x arr[1]`
    
- `Matrix2 = arr[1] x arr[2]`
    
- ...
    
- `Matrix(n-1) = arr[n-2] x arr[n-1]`
    

Find the **minimum number of scalar multiplications** needed to compute the final product of matrices.

---

### ✅ 4. **Recursion with Partitioning**

This is the heart of MCM.

You recursively try:

- All possible positions `k` to split between `i` and `j`
    
- And solve `MCM(i, k)` and `MCM(k+1, j)` recursively
    
- Then combine:  
    `cost = MCM(i, k) + MCM(k+1, j) + arr[i-1] * arr[k] * arr[j]`
    

---

### ✅ 5. **Overlapping Subproblems**

MCM has overlapping subproblems, making it perfect for:

- **Memoization (top-down DP)**
    
- **Tabulation (bottom-up DP)**
    

---

### ✅ 6. **DP Table Meaning**

In tabulation, `dp[i][j]` typically means:

> The **minimum cost** to multiply matrices from `i` to `j`.

---

### ✅ 7. **Base Case**

- When `i == j`, only one matrix: cost = 0.
    

---

### ✅ 8. **Parenthesis Placement (optional)**

- Know how to reconstruct the optimal parenthesization using a `bracket[][]` table (optional but advanced).


1. MCM
2. Printing MCM
3. Evaluate expression to True (Boolean parenthesis)
4. Min/Max value of any expression
5. Palindrome Partitioning
6. Scramble String
7. Egg dropping problem

