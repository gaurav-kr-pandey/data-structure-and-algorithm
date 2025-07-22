Here's a **DSA-focused cheat sheet on XOR (exclusive OR)** — specifically designed for use in **competitive programming**, **interview problems**, and **data structures & algorithms**.

## ✅ 1. What is XOR?

XOR stands for **eXclusive OR**. It's a **bitwise operation**:

- For each bit position:
    - `0 ^ 0 = 0`
    - `1 ^ 1 = 0`
    - `0 ^ 1 = 1`
    - `1 ^ 0 = 1`

It’s true when **only one** of the bits is 1.

---

## 🔹 2. Important XOR Properties (Must Know for DSA)

|Property|Explanation|Use Case|
|---|---|---|
|`a ^ a = 0`|XOR-ing a number with itself gives 0|Cancel duplicates or find unique|
|`a ^ 0 = a`|XOR-ing with 0 doesn't change value|Useful for initializing prefix XOR|
|`a ^ b = c → a = b ^ c`|Rearranging works due to symmetry|Critical in prefix XOR subarray problems|
|XOR is **commutative**|`a ^ b = b ^ a`|Order doesn't matter|
|XOR is **associative**|`(a ^ b) ^ c = a ^ (b ^ c)`|You can group XOR operations|

## 📌 3. Most Important Use Cases in DSA

---
### 1. **Find the Single Element**

Problem: Every number occurs twice except one — find that one.

🔹 Code:

```java
int xor = 0;
for (int num : arr) xor ^= num;
return xor;
```

🔹 Why it works: All duplicates cancel out:  
`a ^ a ^ b ^ b ^ c = 0 ^ 0 ^ c = c`

---

### 2. **Two Elements Appear Once (Others Twice)**

Use overall XOR to split array into 2 groups based on set bits.

🔹 Use: Bitmasking + XOR

---

### 3. **Subarrays with Given XOR**

#### Problem: Count subarrays with XOR = k

🔹 Trick:  
If `prefixXor[j] ^ prefixXor[i-1] = k`, then:

```
prefixXor[i-1] = prefixXor[j] ^ k
```

🔹 Code:

```java
Map<Integer, Integer> freq = new HashMap<>();
freq.put(0, 1);
int xor = 0, count = 0;

for (int num : arr) {
    xor ^= num;
    count += freq.getOrDefault(xor ^ k, 0);
    freq.put(xor, freq.getOrDefault(xor, 0) + 1);
}
```

---

### 4. **Prefix XOR Technique**

- Similar to prefix sum
    
- `prefixXor[i] = arr[0] ^ arr[1] ^ ... ^ arr[i]`
    
- Can be used to find subarray XOR in constant time
    

🔹 Formula:

```java
XOR(i to j) = prefixXor[j] ^ prefixXor[i - 1]
```

---

## 💥 Bonus Tricks & Observations

|XOR Pattern|Result|
|---|---|
|XOR of all numbers from 1 to n (inclusive)|Pattern-based|
|`n % 4 == 0` → `n`||
|`n % 4 == 1` → `1`||
|`n % 4 == 2` → `n + 1`||
|`n % 4 == 3` → `0`|Use in XOR range queries|

---

## 🚫 When XOR Fails

- **Cannot use sliding window** on XOR like you can with sum
    
- Because XOR is **not monotonic**
    
- You can't predict if `xor > k`, then shrinking window will reduce XOR
    

---

## 🧠 Summary for Interviews

|You Should Know|Used For|
|---|---|
|`a ^ a = 0`, `a ^ 0 = a`|Eliminate duplicates|
|`a ^ b = c → a = b ^ c`|Prefix XOR based subarray tricks|
|XOR is associative + commutative|Grouping doesn't matter|
|Prefix XOR pattern|Subarray XOR queries|
|Count subarrays with XOR = k using hashmap|Very common in hard problems|
