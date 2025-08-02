# Problem Statement
You are given an m x n grid where each cell can have one of three values:

    0 representing an empty cell,
    1 representing a fresh orange, or
    2 representing a rotten orange.

Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1.

[Tutorial](https://www.youtube.com/watch?v=Dq3dGS_0Z6o&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=5)

# Thought Process
- Do a BFS
- Use double while loop to count the levels

# Code
```cpp
class Solution {
    int n, m;
public:
    int orangesRotting(vector<vector<int>>& grid) {
        n = size(grid);
        m = size(grid[0]);
        queue<pair<int, int>> q;

        int fresh = 0;
        for(int i = 0; i < n; ++i) {
            for(int j = 0; j < m; ++j) {
                if(grid[i][j] == 2) q.push({i, j});
                if(grid[i][j] == 1) fresh++;
            }
        }
        if(fresh == 0) return 0;
        vector<vector<int>> dir = {{1, 0}, {-1, 0}, {0, -1}, {0, 1}};

        int level_cnt = -1;
        while(!q.empty()) {
            int level_size = size(q);

            if(level_size) level_cnt++;

            while(level_size--) {
                auto f = q.front();
                q.pop();

                for(auto d: dir) {
                    int ni = f.first + d[0];
                    int nj = f.second + d[1];

                    if(ni >= 0 && ni < n && nj >= 0 && nj < m && grid[ni][nj] == 1) {
                        grid[ni][nj] = 2;
                        fresh--;
                        q.push({ni, nj});
                    }
                }
            }
        }

        if(fresh > 0) return -1;

        return level_cnt;
    }
};
```

# Problem Links
- https://leetcode.com/problems/rotting-oranges/