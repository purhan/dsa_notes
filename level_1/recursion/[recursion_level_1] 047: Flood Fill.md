# Problem Statement
1. You are given a number n, representing the number of rows.
2. You are given a number m, representing the number of columns.
3. You are given n*m numbers, representing elements of 2d array a. The numbers can be 1 or 0 only.
4. You are standing in the top-left corner and have to reach the bottom-right corner. 
Only four moves are allowed 't' (1-step up), 'l' (1-step left), 'd' (1-step down) 'r' (1-step right). You can only move to cells which have 0 value in them. You can't move out of the boundaries or in the cells which have value 1 in them (1 means obstacle)
5. Complete the body of floodfill function - without changing signature - to print all paths that can be used to move from top-left to bottom-right.

Note1 -> Please check the sample input and output for details
Note2 -> If all four moves are available make moves in the order 't', 'l', 'd' and 'r'

[Tutorial](https://www.youtube.com/watch?v=R1URUB6_y2k&list=PL-Jc9J83PIiFxaBahjslhBD1LiJAV7nKs&index=47)

# Thought Process

# Code
```cpp
void floodfill(vector<vector<int>>maze, int sr, int sc, int dr, int dc, string psf, vector<vector<bool>> visited) {
    if (sr < 0 || sc < 0 || sr > dr || sc > dc || maze[sr][sc] == 1 || visited[sr][sc]) {
        return;
    }

    if (sr == dr && sc == dc) {
        cout << psf << endl;
        return;
    }
    visited[sr][sc] = true;
    floodfill(maze, sr - 1, sc, dr, dc, psf + "t", visited);
    floodfill(maze, sr, sc - 1, dr, dc, psf + "l", visited);
    floodfill(maze, sr + 1, sc, dr, dc, psf + "d", visited);
    floodfill(maze, sr, sc + 1, dr, dc, psf + "r", visited);
    visited[sr][sc] = false;
}

int main() {
    int n, m;
    cin >> n >> m;
    vector < vector < int >> arr(n, vector < int > (m));

    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            cin >> arr[i][j];

    vector< vector<bool>> visited(n);
    for (auto&it : visited) {
        vector<bool> check(m, false);
        it = check;
    }
    floodfill(arr, 0, 0, n - 1, m - 1, "", visited);
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/recursion-backtracking/flood-fill-official/ojquestion
