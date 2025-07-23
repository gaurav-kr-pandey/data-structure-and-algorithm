**Practice**: [geeksforgeeks](https://www.geeksforgeeks.org/problems/stock-span-problem-1587115621/1)

```java

class Solution {
    public ArrayList<Integer> calculateSpan(int[] arr) {
        
        int n = arr.length;
        Stack<Integer> st = new Stack<>();
        ArrayList<Integer> res = new ArrayList<>();
        int[] index = new int[n];
        
        for (int i = 0; i < n; i++) {
            
            while (!st.isEmpty() && arr[st.peek()] <= arr[i]) {
                st.pop();
            }
            
            int x = st.isEmpty() ? -1 : st.peek();
            index[i] = x;
            res.add(i - x);
            
            st.add(i);
        }
        
        return res;
    }
}

```