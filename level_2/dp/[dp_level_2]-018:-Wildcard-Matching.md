# Problem Statement
1. You are given two strings S1 and S2. S1 represents a text and S2 represents a wildcard pattern.
2. You have to print 'true' if the wildcard pattern is matched with the given text, otherwise print 'false'.

The wildcard pattern can include the characters '?' and '*'
'?' - matches any single character
'*' - matches any sequence of characters (including the empty sequence).

[Tutorial](https://www.youtube.com/watch?v=NbgUZAoIz3g&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=18)

# Thought Process
- Similar to LCS
- Create a 2D DP
![image](https://user-images.githubusercontent.com/10897423/134038963-215cbde9-9007-4f93-8b22-70f861636ff6.png)
- Each cell represents - Do the highlighted patterns match? (true/false)
- We traverse from bottom right to top left
- Observe the behavior of `?` and `*` in the screenshot below, then look at the code
![image](https://user-images.githubusercontent.com/10897423/134045275-81601879-5516-4d79-bf5b-136e001ea95b.png)



# Code
```cpp
class Solution {
public:
    bool isMatch(string str, string pattern) {
        int n = str.length(), m = pattern.length();
        vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));

        for (int i = m; i >= 0; --i) {
            for (int j = n; j >= 0; --j) {
                if (i == m && j == n) {
                    // This cell represents blank v/s blank, which is true
                    dp[i][j] = true;
                } else if (i == m) {
                    // Blank v/s anything else is always false
                    dp[i][j] = false;
                } else if (j == n) {
                    if (pattern[i] == '*') {
                        dp[i][j] = dp[i + 1][j];
                    } else {
                        dp[i][j] = false;
                    }
                } else {
                    if (pattern[i] == '?') {
                        dp[i][j] = dp[i + 1][j + 1];
                    } else if (pattern[i] == '*') {
                        dp[i][j] = dp[i + 1][j] || dp[i][j + 1];
                    } else if (pattern[i] == str[j]) {
                        dp[i][j] = dp[i + 1][j + 1];
                    } else {
                        dp[i][j] = false;
                    }
                }
            }
        }        
        
        return dp[0][0];
    }
};
```

# Problem Links
https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/wildcard-pattern-matching-official/ojquestion  
https://leetcode.com/problems/wildcard-matching/