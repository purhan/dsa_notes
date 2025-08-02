# Problem Statement
1. You are given a string str.
2. You have to find the length of longest subsequence which is appearing twice in the string.
3. Every ith character in both the subsequences must have different indices in the original string.

[Tutorial](https://www.youtube.com/watch?v=oL7GCrcdaJI&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=40)

# Thought Process
- Just find out LCS with itself with one condition:
  - Condition for comparing cells in LCS - Value should be same but index should be different
  - So we just skip cells where index is same

# Code
```cpp
void solve(string s, int n) {
    vector<vector<int>> dp(n + 1, vector<int>(n + 1, 0));

    for (int i = n; i >= 0; --i) {
        for (int j = n; j >= 0; --j) {
            if (i == n || j == n) {
                dp[i][j] = 0;
            } else {
                if (s[i] == s[j] && i != j) {   // Most important step
                    dp[i][j] = dp[i + 1][j + 1] + 1;
                } else {
                    dp[i][j]  = max(dp[i + 1][j], dp[i][j + 1]);
                }
            }
        }
    }

    cout << dp[0][0];
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/longest-repeating-subsequence-official/ojquestion#!
