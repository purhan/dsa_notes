# Problem Statement
1. You are given a number n, representing the size of a n * n chess board.
2. You are required to calculate and print the combinations in which n queens can be placed on the 
     n * n chess-board. 

Note -> Use the code snippet and follow the algorithm discussed in question video. The judge can't 
               force you but the intention is to teach a concept. Play in spirit of the question.

[Tutorial](https://www.youtube.com/watch?v=Ra_fCLyWtr0&list=PL-Jc9J83PIiHO9SQ6lxGuDsZNt2mkHEn0&index=6)

# Thought Process
- Each cell can `either have queen or not have it`
- For the first cell, we can `either place or not place` -> and find answer for the remaining boxes
- To find answer for remaining boxes, if we are on last column, we move to first col of next row
- When whole board has been traversed, we get an arrangement. We print it if it has n queens

# Code
```cpp
void combinations(int n, vector<string>& board, int row, int col, int placedSoFar) {

    if (row == n) {
        if (placedSoFar == n) {
            for (auto r : board) {
                cout << r << "\n";
            }
            cout << "\n";
        }
        return;
    }

    board[row][col] = 'q';
    if (col == n - 1)
        combinations(n, board, row + 1, 0, placedSoFar + 1);
    else
        combinations(n, board, row, col + 1, placedSoFar + 1);

    board[row][col] = '-';
    if (col == n - 1)
        combinations(n, board, row + 1, 0, placedSoFar);
    else
        combinations(n, board, row, col + 1, placedSoFar);
}

void solve(int n) {
    vector<string> board(n, string(n, '-'));
    combinations(n, board, 0, 0, 0);
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/recursion-and-backtracking/queens-combinations-2das2d-box-chooses-official/ojquestion
