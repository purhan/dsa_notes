# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=SXimkBvg50Q&list=PL-Jc9J83PIiFJRioti3ZV7QabwoJK6eKe&index=19)

# Thought Process
- Same recursive approach, just cached using bit masking

# Code
```cpp
class Solution {
    int row[9];
    int col[9];
    int box[3][3];

    bool solve(vector<vector<char>>& board, int r, int c) {
        if(r == 9) {
            return true;
        }
        if(c == 9) {
            return solve(board, r + 1, 0);
        }

        if(board[r][c] != '.') {
            return solve(board, r, c + 1);
        } else {
            for(int i = 1; i <= 9; ++i) {
                if(
                    (row[r] & (1 << i)) == 0 &&
                    (col[c] & (1 << i)) == 0 &&
                    (box[r/3][c/3] & (1 << i)) == 0
                ) {
                    board[r][c] = '0' + i;
                    row[r] ^= (1 << i);
                    col[c] ^= (1 << i);
                    box[r/3][c/3] ^= (1 << i);
                    if(solve(board, r, c + 1)) return true;
                    row[r] ^= (1 << i);
                    col[c] ^= (1 << i);
                    box[r/3][c/3] ^= (1 << i);
                    board[r][c] = '.';
                }
            }
        }

        return false;
    }
public:
    void solveSudoku(vector<vector<char>>& board) {
        for(int i = 0; i < 9; ++i) {
            for(int j = 0; j < 9; ++j) {
                if(board[i][j] != '.') {
                    int num = board[i][j] - '0';
                    row[i] ^= (1 << num);
                    col[j] ^= (1 << num);
                    box[i/3][j/3] ^= (1 << num);
                }
            }
        }

        solve(board, 0, 0);
    }
};
```

# Problem Links
- https://leetcode.com/problems/sudoku-solver/
