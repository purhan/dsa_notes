# Problem Statement

Given a string s. In one step you can insert any character at any index of the string.

Return the minimum number of steps to make s palindrome.

A Palindrome String is one that reads the same backward as well as forward.

[Tutorial](https://www.youtube.com/watch?v=IP4iqrh0mQk&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=64)

# Thought Process
- To convert a string to palindrome, assume we need to make `x` insertions.
- It's same as making `x` deletions, since there were `x` characters in string that didn't have a corresponding character
- To solve, find length of longest palindromic subsequence
- All the remaining characters are not a part of this palindrome, hence need to be removed or added again on opposite end of the string
- So the answer is LPS - x

# Code
```cpp
class Solution {
    vector<vector<int>> dp;

    int lps(string& s, int i, int j) {
        if(i >= j) return 1;
        if(j - i == 1) return (s[i] == s[j] ? 2 : 1);

        if(dp[i][j] != -1) return dp[i][j];

        if(s[i] == s[j]) return dp[i][j] = lps(s, i + 1, j - 1) + 2;
        else {
            int left = lps(s, i + 1, j);
            int right = lps(s, i, j - 1);
            return dp[i][j] = max(left, right);
        }
    }
public:
    int minInsertions(string s) {
        int n = s.size();
        dp = vector<vector<int>>(n + 1, vector<int>(n + 1, -1));
        return n - lps(s, 0, n - 1);
    }
};
```

# Problem Links
- https://leetcode.com/problems/minimum-insertion-steps-to-make-a-string-palindrome/
