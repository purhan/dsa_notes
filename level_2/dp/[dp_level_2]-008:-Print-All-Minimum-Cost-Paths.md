# Problem Statement
1. You are given a number n, representing the number of rows.
2. You are given a number m, representing the number of columns.
3. You are given n*m numbers, representing elements of 2d array a, which represents a maze.
4. You are standing in top-left cell and are required to move to bottom-right cell.
5. You are allowed to move 1 cell right (h move) or 1 cell down (v move) in 1 motion.
6. Each cell has a value that will have to be paid to enter that cell (even for the top-left and bottom-right cell).
7. You are required to traverse through the matrix and print the cost of the path which is least costly.
8. Also, you have to print all the paths with minimum cost.

[Tutorial](https://www.youtube.com/watch?v=f8Vdifn2YjQ&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=8)

# Thought Process

- This is extended version of [Goldmine Problem](https://www.youtube.com/watch?v=5KdvH15NJjc&list=PL-Jc9J83PIiG8fE6rj9F5a6uyQ5WPdqKy&index=8) (aka minimum/maximum cost path)
- First part of the solution is similar to Goldmine Problem

![image](https://user-images.githubusercontent.com/10897423/133956969-9c3b5119-d18c-4002-9898-e397eb33ed08.png)

- Traverse through all paths with minimum cost and store it in a tree
- Do a BFS to print those paths

# Code

```cpp
class Path {
    // Stores ("H", x, y) of a cell
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

    for (int i = n - 1; i >= 0; --i) {
        for (int j = m - 1; j >= 0; --j) {
            if (i == n - 1 && j == m - 1) {
                continue;
            } else if (i == n - 1) {
                dp[i][j] = dp[i][j + 1] + grid[i][j];
            } else if (j == m - 1) {
                dp[i][j] = dp[i + 1][j] + grid[i][j];
            } else {
                dp[i][j] = min(dp[i][j + 1], dp[i + 1][j]);
                dp[i][j] += grid[i][j];
            }
        }
    }

    cout << dp[0][0] << endl;

    //////////////// Till here it was similar to Goldmine Problem ////////////////

    queue<Path*> q;
    Path* x = new Path("", 0, 0);
    q.push(x);

    while (!q.empty()) {
        Path* f = q.front();
        q.pop();

        if (f->x == n - 1 && f->y == m - 1) {
            
            // Reached final destination, just print
            cout << f->psf << endl;
        } else if (f->y == m - 1) {

            // Reached last column, can only go downwards from here
            Path* v = new Path(f->psf + "V", f->x + 1, f->y);
            q.push(v);
        } else if (f->x == n - 1) {

            // Reached last row, can only go towards right from here
            Path* h = new Path(f->psf + "H", f->x, f->y + 1);
            q.push(h);
        } else {

            // Take minimum of Right v/s Down, or take both if both equal
            if (dp[f->x + 1][f->y] < dp[f->x][f->y + 1]) {
                Path* v = new Path(f->psf + "V", f->x + 1, f->y);
                q.push(v);
            } else if (dp[f->x + 1][f->y] > dp[f->x][f->y + 1]) {
                Path* h = new Path(f->psf + "H", f->x, f->y + 1);
                q.push(h);
            } else {
                Path* v = new Path(f->psf + "V", f->x + 1, f->y);
                Path* h = new Path(f->psf + "H", f->x, f->y + 1);
                q.push(v);
                q.push(h);
            }
        }
    }
}
```

# Problem Links
https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/minimum-cost-path-re-official/ojquestion