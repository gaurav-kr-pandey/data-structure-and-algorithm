https://leetcode.com/problems/insert-delete-getrandom-o1/

### Solution:

_**ADD:**_
map - put each `val` and it's `index` - O(1)
list -  add all the elements to access it using index in O(1)

**_REMOVE:_**
`swap(list, lastIndexEle, value to be removed Index)` ==> `list.size() - 1` and `index = map.get(val)`


```java
class RandomizedSet {
    List<Integer> list;
    Map<Integer, Integer> seen;  // val -> index in list
    Random random;

    public RandomizedSet() {
        seen = new HashMap<>();
        list = new ArrayList<>();
        random = new Random();
    }

    public boolean insert(int val) {
        if (seen.containsKey(val)) return false;

        list.add(val);
        seen.put(val, list.size() - 1);
        return true;
    }

    public boolean remove(int val) {
        if (!seen.containsKey(val)) return false;

        int currIndex = seen.get(val);
        int lastIndex = list.size() - 1;
        int lastEle = list.get(lastIndex);

        // Move last element to the index of the element to remove
        list.set(currIndex, lastEle);
        seen.put(lastEle, currIndex);

        // Remove the element
        seen.remove(val);
        list.remove(lastIndex);

        return true;
    }

    public int getRandom() {
        return list.get(random.nextInt(list.size()));
    }
}

```