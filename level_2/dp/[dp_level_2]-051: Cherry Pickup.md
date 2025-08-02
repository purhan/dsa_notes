# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/141472738-6344cacd-c255-497b-8315-4e8b734e09e6.png)

[Tutorial](https://www.youtube.com/watch?v=ZV0sUzfA7Eg&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=53)

# Thought Process

- We have to find the optimal path from start to end and then optimal path from end to start
- However, we can also think of it this way:
  - We have to find optimal way so that two players, starting from (0, 0) reach the end optimally
- Another catch is that we don't need to store column for second player (during memoization, we can avoid using 4-D DP and use 3D Dp instead, because c2=r1+c1-r2 always)
- Think recursively for this problem, then memoize it

# Code
```cpp
class Solution {
    int dp[51][51][51];

    int helper(vector<vector<int>>& grid, int r1, int c1, int r2) {
        int c2 = r1 + c1 - r2;
        if (r1 >= grid.size() || r2 >= grid.size() || c1 >= grid.size() || c2 >= grid.size() || grid[r1][c1] == -1 || grid[r2][c2] == -1) {
            return INT_MIN;
        }

        if(r1 == grid.size() - 1 && c1 == grid.size() - 1) {
            return grid[r1][c1];
        }

        if(dp[r1][c1][r2] != -1) return dp[r1][c1][r2];

        int collected = 0;
        if(r1 == r2 && c1 == c2) {
            collected += grid[r1][c1];
        } else {
            collected += grid[r1][c1] + grid[r2][c2];
        }

        int f1 = helper(grid, r1 + 1, c1, r2 + 1);
        int f2 = helper(grid, r1 + 1, c1, r2);
        int f3 = helper(grid, r1, c1 + 1, r2 + 1);
        int f4 = helper(grid, r1, c1 + 1, r2);

        collected += max({f1, f2, f3, f4});
        return dp[r1][c1][r2] = collected;
    }

public:
    int cherryPickup(vector<vector<int>>& grid) {
        int n = grid.size();
        memset(dp,-1,sizeof(dp));
        return max(helper(grid, 0, 0, 0), 0);
    }
};
```

# Problem Links
- https://leetcode.com/problems/cherry-pickup/
