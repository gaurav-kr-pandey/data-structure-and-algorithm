# Heap Data Structure (Java)

## 📌 Introduction
- **Heap** is a special **binary tree-based data structure** that satisfies the **heap property**.
- A **complete binary tree** → all levels are filled except possibly the last, which is filled left to right.
- **Heap Property**:
  - **Max Heap** → parent node ≥ child nodes.
  - **Min Heap** → parent node ≤ child nodes.

👉 Always implemented as an **array** in practice (not linked nodes).

---
## 📌 Types of Heaps
1. **Max Heap**
   - Root is the **largest** element.
   - Used in **Heap Sort**, **Priority Queues**.
   - Example: `[100, 50, 30, 20, 10, 15]`

2. **Min Heap**
   - Root is the **smallest** element.
   - Used in **Dijkstra’s Algorithm**, **Prim’s Algorithm**.
   - Example: `[10, 20, 15, 30, 40]`

---

## 📌 Representation in Array
- Root stored at index `0`.
- For a node at index `i`:
  - **Left child** → `2 * i + 1`
  - **Right child** → `2 * i + 2`
  - **Parent** → `(i - 1)/2`

---
## 📌 Heap Operations
1. **Insertion**
   - Add element at the end.
   - Perform **Heapify-Up** (bubble up).
   - TC: `O(log n)`.

2. **Deletion (extract root)**
   - Remove root element.
   - Replace root with the last element.
   - Perform **Heapify-Down** (bubble down).
   - TC: `O(log n)`.

3. **Peek (Get root)**
   - Return root element.
   - TC: `O(1)`.

4. **Heapify**
   - Convert array into heap.
   - Bottom-up approach.
   - TC: `O(n)`.

---

## 📌 Time Complexities
| Operation | Time Complexity |
| --------- | --------------- |
| Insert    | `O(log n)`      |
| Delete    | `O(log n)`      |
| Peek      | `O(1)`          |
| Heapify   | `O(n)`          |

---
## 📌 Applications of Heap
- **Priority Queue** implementation.
- **Heap Sort** algorithm.
- **Graph Algorithms**:
	  - Dijkstra’s shortest path. (`Ref:` )
	  - Prim’s  - Minimum Spanning Tree. ( `Ref:` [[13 - Prim's Algorithm]], [[12 - Minimum Spanning Tree]])
- **Median of a stream** (using min-heap & max-heap).
- **Job Scheduling**.

---
## 📌 Heap in Java
Java provides **PriorityQueue** (Min Heap by default).

### Min Heap (default)

```java
import java.util.PriorityQueue;

public class MinHeapExample {
    public static void main(String[] args) {
        PriorityQueue<Integer> minHeap = new PriorityQueue<>();
        
        minHeap.add(10);
        minHeap.add(20);
        minHeap.add(5);
        
        System.out.println(minHeap.peek()); // 5
        System.out.println(minHeap.poll()); // 5 (removes root)
        System.out.println(minHeap.peek()); // 10
    }
}
```

## Max Heap

```java
import java.util.Collections;
import java.util.PriorityQueue;

public class MaxHeapExample {
    public static void main(String[] args) {
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
        
        maxHeap.add(10);
        maxHeap.add(20);
        maxHeap.add(5);
        
        System.out.println(maxHeap.peek()); // 20
        System.out.println(maxHeap.poll()); // 20 (removes root)
        System.out.println(maxHeap.peek()); // 10
    }
}

```

## 📌 Summary

- Heap is a **complete binary tree** with **heap property**.
- Two types: **Max Heap** & **Min Heap**.
- Used in **priority queues, sorting, graph algorithms**.
- In Java → **PriorityQueue** (Min Heap by default).
- Key operations → insert, delete, peek, heapify.