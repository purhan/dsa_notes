# Problem Statement
1. You are given a string str.
2. You are required to print the length of longest palindromic subsequence of string str.

[Tutorial](https://www.youtube.com/watch?v=RiNzHfoA2Lo&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=17)

# Thought Process
- Create a 2D DP

![image](https://user-images.githubusercontent.com/10897423/134154294-d78abbf8-e658-4628-b947-96bb1ac1e1e2.png)

- Each cell stores the Length of Longest Palindromic Subsequence starting and ending at those indices respectively (look at the screenshot)
- At every substring, check if extremes are equal
  - If not, take max of `prefix LPS` and `suffix LPS` (why? check the code / tutorial)
    - For example, if we have `abc`, we check max for `ab` and `bc`
  - If extremes are equal, we check the LPS for the middle part, and add 2 to it because we have 2 new characters (on extremes) that give a palindrome

![image](https://user-images.githubusercontent.com/10897423/134156989-d6f46046-f7de-4491-8365-628c93a6cea2.png)


- Examine the screenshot carefully

# Code
```cpp
class Solution {
public:
    int longestPalindromeSubseq(string str) {
        int ans = 0, n = str.length();
        vector<vector<int>> dp(n, vector<int>(n, 0));

        for (int g = 0; g < n; ++g) {
            for (int i = 0, j = g; j < n; ++i, ++j) {
                if (g == 0) {
                    dp[i][j] = 1;
                } else if (g == 1) {
                    if (str[i] == str[j]) dp[i][j] = 2;
                    else dp[i][j] = 1;
                } else {
                    if (str[i] == str[j]) {
                        dp[i][j] = 2 + dp[i + 1][j - 1];
                    } else {
                        dp[i][j] = max(dp[i][j - 1], dp[i + 1][j]);
                    }
                }

                ans = max(ans, dp[i][j]);
            }
        }

        return ans;
    }
};
```

# Problem Links
https://leetcode.com/problems/longest-palindromic-subsequence/  
https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/lps-official/ojquestion