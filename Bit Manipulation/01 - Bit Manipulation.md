
## ✅ What is Bit Manipulation?

Bit manipulation involves using **bitwise operators** to solve problems efficiently by working directly with binary representations of numbers. It is powerful for optimizing space and time.

---

## 🔹 Bitwise Operators in Java

|Operator|Symbol|Meaning|
|---|---|---|
|AND|`&`|Bitwise AND|
|OR|`|`|
|XOR|`^`|Bitwise XOR|
|NOT|`~`|Bitwise NOT (1's complement)|
|Left Shift|`<<`|Shift bits left|
|Right Shift|`>>`|Shift bits right (sign bit preserved)|
|Unsigned Right Shift|`>>>`|Shift bits right (fill 0 from left)|

---

## 📌 Binary Basics

|Decimal|Binary|
|---|---|
|0|0000|
|1|0001|
|2|0010|
|3|0011|
|4|0100|
|5|0101|

---

## ✅ Essential Bit Tricks & Concepts

### 1. **Check if a number is even or odd**

```java
if ((n & 1) == 0) → even
else → odd
```

### 2. **Multiply or divide by powers of 2**

```java
n << 1 → n * 2
n >> 1 → n / 2
```

### 3. **Check if the ith bit is set**

```java
(n & (1 << i)) != 0
```

### 4. **Set the ith bit**

```java
n = n | (1 << i);
```

### 5. **Clear the ith bit**

```java
n = n & ~(1 << i);
```

### 6. **Toggle the ith bit**

```java
n = n ^ (1 << i);
```

### 7. **Count number of set bits (1s)**

```java
Integer.bitCount(n);
```

---

## 🔥 Advanced Tricks

### 1. **Check if a number is power of 2**

```java
(n > 0) && ((n & (n - 1)) == 0)
```

> Works because power of 2 has only one bit set.

### 2. **Remove the lowest set bit**

```java
n = n & (n - 1);
```

> Useful in Hamming weight and subset problems.

### 3. **Get the lowest set bit only**

```java
n & -n
```

> Isolates the lowest set bit (Two's complement trick).

### 4. **Swap two numbers without temp**

```java
a = a ^ b;
b = a ^ b;
a = a ^ b;
```

### 5. **Gray Code Conversion**

```java
gray = n ^ (n >> 1);
```

---

## 🧠 Summary for Interviews

|Trick|Use Case|
|---|---|
|`n & 1`|Even/Odd check|
|`n & (n - 1)`|Remove lowest set bit|
|`n & -n`|Get lowest set bit|
|`Integer.bitCount(n)`|Count 1s|
|`n << k`, `n >> k`|Multiply/Divide by 2ⁿ|
|`(n & (1 << i)) != 0`|Check if ith bit is set|
|`n|(1 << i)`|
|`n & ~(1 << i)`|Clear ith bit|
|`n ^ (1 << i)`|Toggle ith bit|
|`n ^ (n >> 1)`|Convert to Gray code|

---