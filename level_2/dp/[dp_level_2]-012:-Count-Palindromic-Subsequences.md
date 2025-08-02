# Problem Statement
1. You are given a string str.
2. You are required to print the count of palindromic subsequences in string str.

[Tutorial](https://www.youtube.com/watch?v=YHSjvswCXC8&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=12)

# Thought Process

> **Note:** Coding part is simple, more important is establishing the proof. This solution is incomplete right now, thought process has to be explained, please complete it asap.

# Code
```cpp
int solve(string str) {
    int n = str.length();
    vector<vector<int>> dp(n, vector<int>(n, 0));

    for (int g = 0; g < n; ++g) {

        for (int i = 0, j = g; j < n; ++i, ++j) {
            if (g == 0) {
                dp[i][j] = 1;
            } else if (g == 1) {
                if (str[i] == str[j]) {
                    dp[i][j] = 3;
                } else {
                    dp[i][j] = 2;
                }
            } else {
                if (str[i] == str[j]) {
                    dp[i][j] = dp[i][j - 1] + dp[i + 1][j] + 1;
                } else {
                    dp[i][j] = dp[i][j - 1] + dp[i + 1][j] - dp[i + 1][j - 1];
                }
            }
        }
    }

    return dp[0][n - 1];
}
```

# Problem Links
https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/cps-official/ojquestion  
