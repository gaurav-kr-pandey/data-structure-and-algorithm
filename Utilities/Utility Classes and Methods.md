## 1. Arrays Utilities

```java
int[] arr = {5, 2, 8, 1};

// Sort
Arrays.sort(arr); // ascending
Arrays.sort(arr, 0, 3); // partial sort [0,3)

// Reverse sort (for Integer[], not int[])
Integer[] arr2 = {5, 2, 8, 1};
Arrays.sort(arr2, Collections.reverseOrder());
  
// Binary Search
int idx = Arrays.binarySearch(arr, 2); // returns index if found, else (-insertionPoint-1)

// Fill
Arrays.fill(arr, 7); // fill entire array with 7

// Compare & Equals
boolean eq = Arrays.equals(arr, new int[]{7,7,7,7});

// Copy
int[] copy = Arrays.copyOf(arr, arr.length);
int[] copyRange = Arrays.copyOfRange(arr, 1, 3); // [1,3)
```

  

## 2. Collections Utilities

```java
// List
List<Integer> list = new ArrayList<>(Arrays.asList(1,2,3));
list.add(4);
list.get(0);
list.remove(1); // by index
list.remove(Integer.valueOf(3)); // by value
Collections.sort(list);
Collections.reverse(list);

// Set
Set<Integer> set = new HashSet<>();
set.add(1);
set.contains(2);
set.remove(1);

// Map
Map<Integer, String> map = new HashMap<>();
map.put(1, "A");
map.getOrDefault(2, "NA");
map.containsKey(1);
map.remove(1);

// Queue (FIFO)
Queue<Integer> q = new LinkedList<>();
q.offer(1); q.offer(2);
int first = q.poll(); // remove head
int peek = q.peek(); // get head without removing

// Deque (Double-ended Queue)
Deque<Integer> dq = new ArrayDeque<>();
dq.offerFirst(1);
dq.offerLast(2);
dq.pollFirst();
dq.pollLast();

// Stack
Stack<Integer> st = new Stack<>();
st.push(1);
st.pop();
st.peek();

// PriorityQueue (Heap)
PriorityQueue<Integer> minHeap = new PriorityQueue<>(); // min-heap
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
minHeap.offer(5);
minHeap.offer(2);
int smallest = minHeap.poll(); // 2
```

  

## 3. Sorting & Comparators

```java
int[][] points = {{3,4},{1,2},{5,1}};

// Sort by first element
Arrays.sort(points, (a, b) -> a[0] - b[0]);

// Sort by second element (descending)
Arrays.sort(points, (a, b) -> b[1] - a[1]);

// Sort objects with Comparator
class Pair {
	int x, y;	
	Pair(int x, int y) { this.x = x; this.y = y; }
}

List<Pair> pairs = new ArrayList<>();
pairs.add(new Pair(3,4));
pairs.add(new Pair(1,2));
pairs.sort((p1, p2) -> p1.x - p2.x); // sort by x
```

  

## 4. String Utilities

```java
String s = "leetcode";

// Convert
char[] chars = s.toCharArray();
String t = new String(chars);
  
// Split
String[] parts = s.split("e");
  
// Substring
String sub = s.substring(0, 4); // "leet"

// Reverse
String reversed = new StringBuilder(s).reverse().toString();

// Char operations
for (char c : s.toCharArray()) {
	int idx = c - 'a'; // map 'a'..'z' to 0..25
} 

// Compare
boolean eq = s.equals("leet");
boolean start = s.startsWith("lee");
boolean end = s.endsWith("code");
```

  

## 5. Math Utilities

```java
int min = Math.min(3, 7);
int max = Math.max(3, 7);
int abs = Math.abs(-5);
int pow = (int)Math.pow(2, 10); // 1024
int sqrt = (int)Math.sqrt(16); // 4
int ceil = (int)Math.ceil(2.3); // 3
int floor = (int)Math.floor(2.9); // 2

// GCD & LCM
int gcd(int a, int b) {
	return b == 0 ? a : gcd(b, a % b);
}

int lcm(int a, int b) {
	return a / gcd(a,b) * b;
}
```

  

## 6. Common Patterns

```java
// Prefix Sum
int[] arr = {1,2,3,4};
int n = arr.length;
int[] prefix = new int[n+1];
for (int i = 0; i < n; i++) {
	prefix[i+1] = prefix[i] + arr[i];
}

// range sum [l,r]
int sum = prefix[r+1] - prefix[l];
  
// Binary Search Template
int binarySearch(int[] nums, int target) {

	int l = 0, r = nums.length - 1;
	
	while (l <= r) {
		int mid = l + (r - l)/2;
		if (nums[mid] == target) 
			return mid;
		else if (nums[mid] < target) 
			l = mid + 1;
		else 
			r = mid - 1;
	}
	
	return -1;
}

// Sliding Window Example (max sum of k-length subarray)
int maxSum(int[] nums, int k) {
	int sum = 0, max = 0;
	for (int i=0; i<nums.length; i++) {
		sum += nums[i];
		if (i >= k) 
			sum -= nums[i-k];
		
		if (i >= k-1) 
			max = Math.max(max, sum);
	}

	return max;
}
```

  

## 7. Useful Shortcuts

```java
// Frequency map for array
Map<Integer,Integer> freq = new HashMap<>();
for (int num : arr) {
	freq.put(num, freq.getOrDefault(num, 0) + 1);
}

// Frequency for characters
int[] count = new int[26];
for (char c : s.toCharArray()) {
	count[c - 'a']++;
}

// Convert List<Integer> -> int[]
int[] nums = list.stream().mapToInt(i->i).toArray();
  
// Convert int[] -> List<Integer>
List<Integer> newList = Arrays.stream(nums).boxed().toList();

// Max element in collection
int maxVal = Collections.max(list);
int minVal = Collections.min(list);
```