# Problem Statement
1. You are given a string.
2. You have to find the minimum number of cuts required to convert the given string into palindromic partitions.
3. Partitioning of the string is a palindromic partitioning if every substring of the partition is a palindrome.

[Tutorial](https://www.youtube.com/watch?v=qmTtAbOTqcg&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=28)

# Thought Process
- Tutorial explains 2 methods, only the optimized one is written here
- This requires 2 DP tables
- Create one to store `is_palindrome`
- The other table uses cut strategy to find minimum cuts to form a palindrome

# Code
```cpp
class Solution {
public:
    int minCut(string s) {
        int n = size(s);

        bool isPalindrome[2001][2001] = {0};

        for(int g = 0; g < n; ++g) {
            for(int i = 0, j = g; j < n; ++i, ++j) {
                if(g == 0) {
                    isPalindrome[i][j] = true;
                } else if(g == 1) {
                    if(s[i] == s[j]) {
                        isPalindrome[i][j] = true;
                    }
                } else {
                     if(s[i] == s[j]) {
                         if(isPalindrome[i + 1][j - 1] == true)
                             isPalindrome[i][j] = true;
                     }
                }
            }
        }

        vector<int> dp(n, 0);

        for(int j = 1; j < n; j++) {
            if(isPalindrome[0][j]) {
                dp[j] = 0;
            } else {
                int mn = INT_MAX - 1;
                for(int i = j; i >= 1; i--) {
                    if(isPalindrome[i][j]) {
                        mn = min(mn, dp[i - 1]);
                    }
                }

                dp[j] = mn + 1;
            }
        }

        return dp[n - 1];
    }
};
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/min-palindromic-cut-official/ojquestion
- https://leetcode.com/problems/palindrome-partitioning-ii/
