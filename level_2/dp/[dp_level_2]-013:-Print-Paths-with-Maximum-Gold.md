# Problem Statement
1. You are given a number n, representing the number of rows.
2. You are given a number m, representing the number of columns.
3. You are given n*m numbers, representing elements of 2d array a, which represents a gold mine.
4. You are standing in front of left wall and are supposed to dig to the right wall. You can start from any row in the left wall.
5. You are allowed to move 1 cell right-up (d1), 1 cell right (d2) or 1 cell right-down(d3).
6. Each cell has a value that is the amount of gold available in the cell.
7. You are required to identify the maximum amount of gold that can be dug out from the mine.
8. Also, you have to print all paths with maximum gold.

[Tutorial](https://www.youtube.com/watch?v=mme6Tqj8tyY&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=13)

# Thought Process

# Code
```cpp
class Path {
public:
    string psf;
    int x;
    int y;

    Path(string path, int i, int j) {
        this->x = i;
        this->y = j;
        this->psf = path;
    }
};

void solve(vector<vector<int>> grid, int n, int m) {
    vector<vector<int>> dp(n, vector<int>(m, 0));
    dp[n - 1][m - 1] = grid[n - 1][m - 1];

    for (int j = m - 1; j >= 0; --j) {
        for (int i = 0; i < n; ++i) {
            if (j == m - 1) {
                dp[i][j] = grid[i][j];
            } else if (i == n - 1) {
                dp[i][j] = grid[i][j] + max(dp[i][j + 1], dp[i - 1][j + 1]);
            } else if (i == 0) {
                dp[i][j] = grid[i][j] + max(dp[i][j + 1], dp[i + 1][j + 1]);
            } else {
                dp[i][j] = grid[i][j] + max({
                    dp[i][j + 1],
                    dp[i + 1][j + 1],
                    dp[i - 1][j + 1]
                });
            }
        }
    }

    int mx = 0;
    for (int i = 0; i < n; ++i) {
        mx = max(mx, dp[i][0]);
    }
    cout << mx << endl;

    queue<Path> q;
    for (int i = n - 1; i >= 0; --i) {
        if (dp[i][0] == mx) {
            q.push(Path(to_string(i), i, 0));
        }
    }

    while (!q.empty()) {
        Path f = q.front();
        q.pop();

        if (f.y == m - 1) {
            cout << f.psf << endl;
        } else if (f.x == n - 1) {
            int g = max(dp[f.x][f.y + 1], dp[f.x - 1][f.y + 1]);

            if (g == dp[f.x][f.y + 1]) {
                q.push(Path(f.psf + " d2", f.x, f.y + 1));
            }
            if (g == dp[f.x - 1][f.y + 1]) {
                q.push(Path(f.psf + " d1", f.x - 1, f.y + 1));
            }
        } else if (f.x == 0) {
            int g = max(dp[f.x][f.y + 1], dp[f.x + 1][f.y + 1]);

            if (g == dp[f.x][f.y + 1]) {
                q.push(Path(f.psf + " d2", f.x, f.y + 1));
            }
            if (g == dp[f.x + 1][f.y + 1]) {
                q.push(Path(f.psf + " d3", f.x + 1, f.y + 1));
            }
        } else {
            int g = max({dp[f.x][f.y + 1], dp[f.x - 1][f.y + 1], dp[f.x + 1][f.y + 1]});

            if (g == dp[f.x][f.y + 1]) {
                q.push(Path(f.psf + " d2", f.x, f.y + 1));
            }
            if (g == dp[f.x - 1][f.y + 1]) {
                q.push(Path(f.psf + " d1", f.x - 1, f.y + 1));
            }
            if (g == dp[f.x + 1][f.y + 1]) {
                q.push(Path(f.psf + " d3", f.x + 1, f.y + 1));
            }
        }
    }
}
```

# Problem Links
https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/goldmine-re-official/ojquestion