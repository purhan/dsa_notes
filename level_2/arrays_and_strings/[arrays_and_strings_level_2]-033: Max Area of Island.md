# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138418129-f1454957-7b2b-489d-82d6-f8027e25b2cc.png)

[Tutorial]()

# Thought Process
- Simple and straightforward. Think!

# Code
```cpp
class Solution {
    void dfs(vector<vector<int>>& grid, vector<vector<bool>>& visited, int i, int j, int n, int m, int& ans, int &max_so_far) {
        if(i < 0 || j < 0 || i >= n || j >= m) return;
        if(visited[i][j]) return;
        if(grid[i][j] == 0) return;
        visited[i][j] = 1;

        max_so_far++;

        dfs(grid, visited, i + 1, j, n, m, ans, max_so_far);
        dfs(grid, visited, i, j + 1, n, m, ans, max_so_far);
        dfs(grid, visited, i - 1, j, n, m, ans, max_so_far);
        dfs(grid, visited, i, j - 1, n, m, ans, max_so_far);
    }
public:
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        int n = grid.size(), m = grid[0].size();
        vector<vector<bool>> visited(n, vector<bool>(m, false));
        int ans = 0;

        for(int i = 0; i < n; ++i) {
            for(int j = 0; j < m; ++j) {
                if(grid[i][j] == 1) {
                    int number_of_elements = 0;
                    dfs(grid, visited, i, j, n, m, ans, number_of_elements);
                    ans = max(ans, number_of_elements);
                }
            }
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/max-area-of-island/
