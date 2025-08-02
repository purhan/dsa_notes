# Problem Statement
1. You are given a number n, representing the size of a n * n chess board.
2. You are required to calculate and print the permutations in which n queens can be placed on the 
     n * n chess-board. 

Note -> Use the code snippet and follow the algorithm discussed in question video. The judge can't 
               force you but the intention is to teach a concept. Play in spirit of the question.

[Tutorial](https://www.youtube.com/watch?v=5ujm7QQUwhs&list=PL-Jc9J83PIiHO9SQ6lxGuDsZNt2mkHEn0&index=9)

# Thought Process
- Same question solved earlier, here instead of choosing a box for each queen, we choose a queen (or no queen) for each box

- Each cell can `either have queen or not have it`
- For the first cell, we can `either place nothing, or place one out of n queens` -> and find answer for the remaining boxes
- To find answer for remaining boxes, if we are on last column, we move to first col of next row
- When whole board has been traversed, we get an arrangement. We print it if it has *n queens placed so far*

# Code
```cpp
void printBoard(vector<vector<int>>& board) {
    for (auto r : board) {
        for (int i = 0; i < (int)r.size(); ++i) {
            int c = r[i];
            if (c == 0) {
                cout << "-";
                if (i != (int)r.size() - 1)
                    cout << "\t";
            } else {
                cout << "q" << c;
                if (i != (int)r.size() - 1)
                    cout << "\t";
            }
        }
        cout << "\n";
    }
    cout << "\n\n";
}

void permute(int n, vector<vector<int>>& board, vector<bool>& used, int row, int col, int queens_placed_so_far) {

    if (col == n) {
        col = 0; row++;
    }

    if (row >= n) {
        if (queens_placed_so_far == n) {
            printBoard(board);
        }
        return;
    }

    for (int i = 1; i <= n; ++i) {
        if (!used[i]) {
            used[i] = true;
            board[row][col] = i;
            permute(n, board, used, row, col + 1, queens_placed_so_far + 1);
            board[row][col] = 0;
            used[i] = false;
        }
    }

    permute(n, board, used, row, col + 1, queens_placed_so_far);
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/recursion-and-backtracking/queens-permutations-2das2d-box-chooses-official/ojquestion
