# Problem Statement
Given an m x n binary matrix mat, return the distance of the nearest 0 for each cell.

The distance between two adjacent cells is 1.

[Tutorial](https://www.youtube.com/watch?v=BJbaUH9dN24&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=5)

# Thought Process
- Do a reverse-BFS from cells that have a zero
- Update the distance whenever you encounter a cell that had a `1` (which you have marked as -1 to avoid conflict with 1 distance)

# Code
```cpp
class Solution {
    int n, m;
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        n = size(mat);
        m = size(mat[0]);

        queue<pair<int, int>> q;

        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                if (mat[i][j] == 0) {
                    q.push({i, j});
                } else {
                    mat[i][j] = -1;
                }
            }
        }

        vector<vector<int>> dir{{ -1, 0}, {0, 1}, {1, 0}, {0, -1}};

        while (!q.empty()) {
            pair<int, int> p = q.front();
            q.pop();

            for (int i = 0; i < 4; i++) {
                int ni = p.first + dir[i][0];
                int nj = p.second + dir[i][1];
                if (ni >= 0 && ni < mat.size() && nj >= 0 && nj < mat[0].size() && mat[ni][nj] == -1) {
                    mat[ni][nj] = mat[p.first][p.second] + 1;
                    q.push({ni, nj});
                }
            }
        }
        return mat;
    }
};
```

# Problem Links
- https://leetcode.com/problems/01-matrix/
