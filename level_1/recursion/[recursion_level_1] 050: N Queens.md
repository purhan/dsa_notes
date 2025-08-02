# Problem Statement
1. You are given a number n, the size of a chess board.
2. You are required to place n number of queens in the n * n cells of board such that no queen can kill another.
Note - Queens kill at distance in all 8 directions
3. Complete the body of printNQueens function - without changing signature - to calculate and print all safe configurations of n-queens. Use sample input and output to get more idea.

Note -> The online judge can't force you to write the function recursively but that is what the spirit of question is. Write recursive and not iterative logic. The purpose of the question is to aid learning recursion and not test you.

[Tutorial](https://www.youtube.com/watch?v=05y82cP3bJo&list=PL-Jc9J83PIiFxaBahjslhBD1LiJAV7nKs&index=51)

> Try the LC version too!! Also revision is important!!

# Thought Process

# Code
```cpp
bool isSafe(vector<vector<int>>chess, int row, int col) {
    //for checking row-wise
    for (int i = row - 1; i >= 0; i--) {
        if (chess[i][col]) {
            return false;
        }
    }

    //for checking left diagonal wise
    int i = row - 1;
    int j = col - 1;
    while (i >= 0 && j >= 0) {
        if (chess[i--][j--]) {
            return false;
        }
    }

    //for checking right diagonal wise
    i = row - 1;
    j = col + 1;
    while (i >= 0 && j < chess.size()) {
        if (chess[i--][j++]) {
            return false;
        }
    }

    return true;
}

vector<vector<char>> n_queens(vector<vector<int>> chess, string qsf, int row) {
    if (row == (int)chess.size()) {
        cout << qsf << "." << endl;
        return;
    }

    for (int col = 0; col < (int)chess.size(); ++col) {
        if (isSafe(chess, row, col)) {
            chess[row][col] = 1;
            n_queens(chess, qsf + to_string(row) + "-" + to_string(col) + ", ", row + 1);
            chess[row][col] = 0;
        }
    }
}

void solve(int n) {
    n_queens(vector<vector<int>>(n, vector<int>(n)), "", 0);
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/recursion-backtracking/n-queens-official/ojquestion
- https://leetcode.com/problems/n-queens/