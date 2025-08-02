# Problem Statement

You are given an m x n integer matrix grid, and three integers row, col, and color. Each value in the grid represents the color of the grid square at that location.

Two squares belong to the same connected component if they have the same color and are next to each other in any of the 4 directions.

The border of a connected component is all the squares in the connected component that are either 4-directionally adjacent to a square not in the component, or on the boundary of the grid (the first or last row or column).

You should color the border of the connected component that contains the square grid[row][col] with color.

Return the final grid.

[Tutorial](https://www.youtube.com/watch?v=R3AJoOBVAlg&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ)

# Thought Process
- Classical floodfill
- Only variation from floodfill-> Check whether the cell is on the border of the colorable area
- To check:
  - Check if all 4 neighbors of the cell are of the same island. If that is not 4, that means cell is on the border

# Code

> My code is a little dirty. Youtube had better code in Java

```cpp
class Solution {
    vector<vector<int>> visited;
    vector<pair<int, int>> toColor;
    int n, m;

    void dfs(vector<vector<int>> grid, int row, int col) {
        int cnt = 0;
        int x = grid[row][col];

        if(visited[row][col]) return;
        visited[row][col] = 1;

        if(row < n - 1 && abs(grid[row + 1][col]) == x) cnt++;
        if(row > 0 && abs(grid[row - 1][col]) == x) cnt++;
        if(col < m - 1 && abs(grid[row][col + 1]) == x) cnt++;
        if(col > 0 && abs(grid[row][col - 1]) == x) cnt++;

        if(cnt != 4) {
            toColor.push_back({row, col});
        }
        if(row < n - 1 && abs(grid[row + 1][col]) == x)
            dfs(grid, row + 1, col);
        if(col < m - 1 && abs(grid[row][col + 1]) == x)
            dfs(grid, row, col + 1);
        if(row > 0 && abs(grid[row - 1][col]) == x)
            dfs(grid, row - 1, col);
        if(col > 0 && abs(grid[row][col - 1]) == x)
            dfs(grid, row, col - 1);
    }

public:
    vector<vector<int>> colorBorder(vector<vector<int>>& grid, int row, int col, int color) {
        n = grid.size(), m = grid[0].size();
        visited.assign(n, vector<int>(m, 0));
        dfs(grid, row, col);

        for(auto i: toColor) {
            grid[i.first][i.second] = color;
        }

        return grid;
    }
};
```

# Problem Links
- https://leetcode.com/problems/coloring-a-border/
