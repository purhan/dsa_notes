# Problem Statement

You are given an m x n binary matrix grid, where 0 represents a sea cell and 1 represents a land cell.

A move consists of walking from one land cell to another adjacent (4-directionally) land cell or walking off the boundary of the grid.

Return the number of land cells in grid for which we cannot walk off the boundary of the grid in any number of moves.

[Tutorial](https://www.youtube.com/watch?v=TXyKxUmj5XU&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=2)

# Thought Process
- Classical floodfill variation
- First, run DFS for cells on the edges, and turn those connected components into zero
- Next, count the remaining 1's in the grid

# Code
```cpp
class Solution {
    vector<vector<int>> visited;
    int n, m;

    void dfs(vector<vector<int>>& grid, int row, int col) {
        if(row == n || col == m || row < 0 || col < 0) return;
        if(grid[row][col] == 0) return;
        if(visited[row][col]) return;
        visited[row][col] = 1;

        dfs(grid, row + 1, col);
        dfs(grid, row, col + 1);
        dfs(grid, row - 1, col);
        dfs(grid, row, col - 1);
    }

public:
    int numEnclaves(vector<vector<int>>& grid) {
        n = grid.size();
        m = grid[0].size();
        visited.assign(n, vector<int>(m, 0));

        for(int i = 0; i < m; ++i) {
            dfs(grid, 0, i);
            dfs(grid, n - 1, i);
        }

        for(int i = 0; i < n; ++i) {
            dfs(grid, i, 0);
            dfs(grid, i, m - 1);
        }

        int ans = 0;
        for(int i = 0; i < n; ++i) {
            for(int j = 0; j < m; ++j) {
                ans += grid[i][j];
                ans -= visited[i][j];
            }
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/coloring-a-border/
