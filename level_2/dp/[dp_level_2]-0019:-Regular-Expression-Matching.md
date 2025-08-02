# Problem Statement
1. You are given two strings S1 and S2. S1 represents a text and S2 represents a pattern.
2. You have to print 'true' if the pattern is matched with the given text, otherwise print 'false'.

The pattern can include the characters '.' and '*'
'.' - matches any single character
'*' - matches zero or more of the preceding character

[Tutorial](https://www.youtube.com/watch?v=DJvw8jCmxUU&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=19)

# Thought Process

Similar to Wildcard, but I should update this section, quite a few things are different.

![image](https://user-images.githubusercontent.com/10897423/134203536-53141639-2a06-4663-9e8a-ff977e4b2337.png)

# Code

> :warning::warning::warning: Code is wrong, update it asap :warning::warning::warning: 

```cpp
void solve(string str, string pat) {
    int n = str.length(), m = pat.length();

    vector<vector<bool>> dp(n + 1, vector<bool>(m + 1, false));

    for (int i = 0; i <= n; ++i) {
        for (int j = 0; j <= m; ++j) {
            if (i == 0 && j == 0) {
                dp[i][j] = true;
            } else if (i == 0) {
                dp[i][j] = false;
            } else if (j == 0) {
                if (pat[i - 1] == '*') {
                    dp[i][j] = dp[i - 2][j];
                } else {
                    dp[i][j] = false;
                }
            } else {
                char pc = pat[i - 1];
                char sc = str[j - 1];

                if (pc == '*') {
                    dp[i][j] = dp[i - 2][j];

                    if (pat[i - 2] == '.' || pat[i - 2] == sc) {
                        dp[i][j] = dp[i][j] || dp[i][j - 1];
                    }
                } else if (pc == '.') {
                    dp[i][j] = dp[i - 1][j - 1];
                } else if (pc == sc) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = false;
                }
            }
        }
    }

    cout << (dp[n][m] ? "true" : "false");
}
```

# Problem Links
https://leetcode.com/problems/regular-expression-matching/

