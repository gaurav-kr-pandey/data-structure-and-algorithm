https://leetcode.com/problems/number-of-provinces/

There are `n` cities. Some of them are connected, while some are not. If city `a` is connected directly with city `b`, and city `b` is connected directly with city `c`, then city `a` is connected indirectly with city `c`.

A **province** is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the `ith` city and the `jth` city are directly connected, and `isConnected[i][j] = 0` otherwise.

Return _the total number of **provinces**_.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg)

**Input:** isConnected = [[1,1,0],[1,1,0],[0,0,1]]
**Output:** 2

### Solution:

This problem is same as number of connected components.


```java
class Solution {
    public int findCircleNum(int[][] isConnected) {
        int n = isConnected.length;
        boolean[] visited = new boolean[n];
        int provinces = 0;

        for (int city = 0; city < n; city++) {
            if (!visited[city]) {
                dfs(isConnected, visited, city);
                provinces++;
            }
        }

        return provinces;
    }

    private void dfs(int[][] graph, boolean[] visited, int node) {
        visited[node] = true;
        for (int neighbor = 0; neighbor < graph.length; neighbor++) {
            if (graph[node][neighbor] == 1 && !visited[neighbor]) {
                dfs(graph, visited, neighbor);
            }
        }
    }
}

```