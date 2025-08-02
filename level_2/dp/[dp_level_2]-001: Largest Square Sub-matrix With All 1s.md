# Problem Statement
1. You are given a matrix of 0's and 1's.
2. You have to find the maximum size square sub-matrix with all 1's.

[Tutorial](https://www.youtube.com/watch?v=UagRoA3C5VQ&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=1)

# Thought Process
- Create a 2D DP of size same as that of the given matrix
- Traverse from bottom-right to top left

![image](https://user-images.githubusercontent.com/10897423/134654751-bd457216-deaf-43ee-85b8-0d40a9235f78.png)

![image](https://user-images.githubusercontent.com/10897423/134656980-e3a71580-18d0-4a92-ac87-20cdaa0150e2.png)

- Skip all the cells that have a `0` in them since they dont contribute to squares
- For each cell, take `min` of right, down and right-down cell. This tells us the maximum sized square that starts from that cell


# Code
```cpp
void solve(vector<vector<int>> mat, int n, int m) {
    vector<vector<int>> dp(n, vector<int>(m));

    int mx = 0;
    for (int i = n - 1; i >= 0; --i) {
        for (int j = m - 1; j >= 0; --j) {

            if (mat[i][j] == 0) continue;   // Such cells don't ever get included in a square

            if (j == m - 1 && i == n - 1) { // Last Cell
                dp[i][j] = 1;
            } else if (j == m - 1) {        // Last Row
                dp[i][j] = 1;
            } else if (i == n - 1) {        // Last Column
                dp[i][j] = 1;
            } else {

                dp[i][j] = min({dp[i + 1][j], dp[i][j + 1], dp[i + 1][j + 1]}) + 1;

            }

            mx = max(mx, dp[i][j]);
        }
    }

    cout << mx << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/largest-square-sub-matrix-with-all-ones-official/ojquestion
