# Problem Statement
1. You are given a number n, representing the size of a n * n chess board.
2. You are required to calculate and print the permutations in which n queens can be placed on the 
     n * n chess-board.

[Tutorial](https://www.youtube.com/watch?v=mkl6KOwtdbk&list=PL-Jc9J83PIiHO9SQ6lxGuDsZNt2mkHEn0&index=5)

# Thought Process
- For every cell in the grid, we mark the queen and recurse for the remaining grid for the next queen
- We reset the cell during backtracking

# Code
```cpp
void printBoard(vector<vector<int>>& board) {
    for (auto r : board) {
        for (auto c : r) {
            if (c == 0) cout << "-\t";
            else cout << 'q' << c << "\t";
        }
        cout << "\n";
    }
    cout << "\n";
}

void permute(int qsf, vector<vector<int>>& board, int n) {
    if (qsf == n + 1) {
        printBoard(board);
    }

    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            if (board[i][j] == 0) {
                board[i][j] = qsf;
                permute(qsf + 1, board, n);
                board[i][j] = 0;
            }
        }
    }
}

void solve(int n) {
    vector<vector<int>> board(n, vector<int>(n, 0));
    permute(1, board, n);
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/recursion-and-backtracking/queens-permutations-2das2d-queen-chooses-official/ojquestion#!
