
## 📌 Heap Basics
- Heap = **Complete Binary Tree** + **Heap Property**.
- Types:
	- **Max Heap** → `Parent ≥ Children`
	- **Min Heap** → `Parent ≤ Children`

👉 Stored as an **array**, you can access left child, right child and parent using formula below:
- Left child = `2 * i + 1`
- Right child = `2 * i + 2`
- Parent = `(i - 1) / 2`

---
## 📌 Min Heap Example

Array: `[10, 20, 15, 30, 40]`

```
	    10
	  /    \
	 20    15
    /  \
   30  40
```

---
## 📌 Max Heap Example

Array: `[100, 50, 30, 20, 10, 15]`

```
	    100
	  /     \
	 50      30
    /  \     /
   20  10   15
```

---
## 📌 Insertion (Heapify Up)

Steps:
1. Insert at last position.
2. Compare with parent → **swap if violates heap property**.
3. Repeat until heap property holds.

Example (Insert 5 into Min Heap `[10, 20, 15, 30, 40]`):

```
Step 1: Insert at end
	     10
	   /    \
	  20     15
     /  \    /
    30  40  5

Step 2: Compare with parent (15) → Swap
	      10
	    /     \
	   20      5
	 /   \    /
	30   40  15
```

---
## 📌 Deletion (Extract Root + Heapify Down)

Steps:
1. Replace root with last element.
2. Remove last element.
3. Heapify down → swap with smaller child (Min Heap).

Example (Delete `10` from `[10, 20, 15, 30, 40]`):

```
Step 1: Replace root with last element

			 40
           /     \
		  20      15
		/
	   30

Step 2: Heapify down

			   15
			 /    \
			20    40
		   /
		  30
```

---
## 📌 Heapify (Build Heap from Array)

Bottom-up method: start from last non-leaf node → heapify down.
Array: `[30, 10, 50, 20, 60]`  

```

Initial:
	    30
	  /    \
	 10     50
    /  \
   20   60

Heapify result (Min Heap):

	       10
	      /  \
    	20     50
	   /  \
      30  60
```

---
## 📌 Time Complexity

| Operation | TC       |
| --------- | -------- |
| Insert    | O(log n) |
| Delete    | O(log n) |
| Peek      | O(1)     |
| Heapify   | O(n)     |

---
## 📌 Use Cases

- Priority Queue
- Heap Sort
- Dijkstra’s Algorithm
- Prim’s Algorithm
- Median in Data Stream
- Job Scheduling