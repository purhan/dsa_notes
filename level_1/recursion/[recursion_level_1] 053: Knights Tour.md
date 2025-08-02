# Problem Statement
1. You are given a number n, the size of a chess board.
2. You are given a row and a column, as a starting point for a knight piece.
3. You are required to generate the all moves of a knight starting in (row, col) such that knight visits all cells of the board exactly once.
4. Complete the body of printKnightsTour function - without changing signature - to calculate and print all configurations of the chess board representing the route of knight through the chess board. Use sample input and output to get more idea.

Note -> When moving from (r, c) to the possible 8 options give first precedence to (r - 2, c + 1) and move in clockwise manner to explore other options.
Note -> The online judge can't force you to write the function recursively but that is what the spirit of question is. Write recursive and not iterative logic. The purpose of the question is to aid learning recursion and not test you.

[Tutorial](https://www.youtube.com/watch?v=SP880DBRJ_8&list=PL-Jc9J83PIiFxaBahjslhBD1LiJAV7nKs&index=53)

# Thought Process

# Code
```cpp
void displayBoard(vector<vector<int>> chess) {
    for (auto& it : chess) {
        for (auto& z : it) {
            cout << z << " ";
        }
        cout << endl;
    }
    cout << endl;
}

void KnightsTour(vector<vector<int>> chess, int r, int c, int move) {

    if (r < 0 || c < 0 || r >= chess.size() || c >= chess.size() || chess[r][c] > 0) {
        return;
    }

    else if (move == chess.size()*chess.size()) {
        chess[r][c] = move;
        displayBoard(chess);
        chess[r][c] = 0;
        return;
    }

    chess[r][c] = move;
    KnightsTour(chess, r - 2, c + 1, move + 1);
    KnightsTour(chess, r - 1, c + 2, move + 1);
    KnightsTour(chess, r + 1, c + 2, move + 1);
    KnightsTour(chess, r + 2, c + 1, move + 1);
    KnightsTour(chess, r + 2, c - 1, move + 1);
    KnightsTour(chess, r + 1, c - 2, move + 1);
    KnightsTour(chess, r - 1, c - 2, move + 1);
    KnightsTour(chess, r - 2, c - 1, move + 1);
    chess[r][c] = 0;
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/recursion-backtracking/knights-tour-official/ojquestion
