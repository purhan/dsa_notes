# Problem Statement
Given an m*n binary matrix mat, return the number of distinct island.

An island is considered to be the same as another if and only if one island can be translated (and not rotated or reflected) to equal the other.

[Tutorial](https://www.youtube.com/watch?v=4vY_ZPi9jTs&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=3)

# Thought Process
- Do a DFS on all connected components
- Store the DFS traversal in a set, return the size of the set in the end

- To store the traversal, *read the code*. Also remember to add a 'b' when backtracking

# Code
```cpp
vector<vector<int>> grid;
vector<vector<int>> visited;
set<string> hashset;
int n, m;
string psf;

void dfs(int row, int col, char ch) {
    if (row < 0 || col < 0 || row == n || col == m) return;
    if (grid[row][col] == 0) return;
    if (visited[row][col]) return;
    visited[row][col] = 1;
    psf += ch;

    dfs(row + 1, col, 'd');
    dfs(row - 1, col, 'u');
    dfs(row, col + 1, 'r');
    dfs(row, col - 1, 'l');
    psf += 'b';
}

void solve() {
    cin >> n >> m;
    grid.assign(n, vector<int>(m, 0));
    visited.assign(n, vector<int>(m, 0));

    for (int i = 0; i < n; ++i) for (int j = 0; j < m; ++j) cin >> grid[i][j];

    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < m; ++j) {
            psf = "";
            dfs(i, j, '0');
            if (sz(psf) > 0)
                hashset.insert(psf);
        }
    }

    cout << sz(hashset);
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/number-of-distinct-island-official/ojquestion
