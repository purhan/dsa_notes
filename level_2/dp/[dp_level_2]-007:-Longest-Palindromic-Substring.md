# Problem Statement
1. You are given a string string.
2. You are required to print the length of longest of palindromic substrings in string string.

[Tutorial](https://www.youtube.com/watch?v=WpYHNHofwjc&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=7)

# Thought Process

Same as DP Level 2 - 6 Count of Palindromic Substrings

# Code

```cpp
int solve(string str) {
    int n = str.length(), ans = 0;
    vector<vector<bool>> dp(n, vector<bool>(n, false));

    for (int g = 0; g < n; ++g) {
        for (int i = 0, j = g; j < n; ++j, ++i) {
            if (g == 0) {
                dp[i][j] = true;
            } else if (g == 1) {
                dp[i][j] = (str[i] == str[j]);
            } else {
                dp[i][j] = (str[i] == str[j]) && dp[i + 1][j - 1];
            }

            if (dp[i][j]) 
                ans = max(ans, g + 1);  // Can store ans = g + 1 directly without comparing since we are always traversing towards larger gap
        }
    }

    return ans;
}
```

# Problem Links
https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/lpss-official/ojquestion