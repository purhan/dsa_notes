# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/144419392-4c1dd4e9-a1fb-4740-bce0-3c5e78cd6a4a.png)

[Tutorial](https://www.youtube.com/watch?v=54nJhM2AZv4&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=63)

# Thought Process
- I thought of a recursive solution but that gave TLE
- Instead, use 2D arrays and simulate using them

# Code
```cpp
class Solution {
public:
    vector<vector<int>> dir = {{-1, 2}, {-2, 1}, {-1, -2}, {-2, -1}, {1, 2}, {2, 1}, {1, -2}, {2, -1}};

    bool isLegal(int r, int c, int n) {
        return !(r < 0 || c < 0 || r >= n || c >= n);
    }

///////////////////////////////////////////////////////////////////////////////////////////////////////////////////

    double knightProbability(int n, int k, int row, int col) {

        // create a board for simulation
        vector<vector<double>> parentBoard(n, vector<double>(n));
        parentBoard[row][col] = 1;  // initially at this cell

        for(int t = 0; t < k; ++t) {

            vector<vector<double>> childBoard(n, vector<double>(n));

            for(int i = 0; i < n; ++i) {
                for(int j = 0; j < n; ++j) {

                    double moveProb = parentBoard[i][j] / 8.0;

                    for(auto d: dir) {
                        int nrow = i + d[0];
                        int ncol = j + d[1];

                        if(isLegal(nrow, ncol, n)) childBoard[nrow][ncol] += moveProb;
                    }
                }
            }
            parentBoard = childBoard;
        }

        // have to return probability for whole board, so find out just that
        double ans = 0;
        for(int p = 0; p < n; p++)
            for(int q = 0; q < n; q++)
                   ans += parentBoard[p][q];

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/knight-probability-in-chessboard/
