# Problem Statement
1. You are given a string str1.
2. You are given another string str2.
3. You are required to print the length of longest common subsequence of two strings.

[Tutorial](https://www.youtube.com/watch?v=0Ql40Llp09E&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=17)

# Thought Process
- Create a 2D DP
- Each cell stores the LCS till that cell
![image](https://user-images.githubusercontent.com/10897423/134048892-1429a670-8ed2-495b-a160-2953443ffae1.png)
- In case `s1[i] == s2[j]` we check the diagonal next, and add 1. Simply, we check the remaining strings and whether they match
- In case `s1[i] != s2[j]` we take max(dp[i + 1][j], dp[i][j + 1]). Simply, we check the last LCS before that cell


# Code
```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int l1 = text1.length(), l2 = text2.length();
        vector<vector<int>> dp(l1 + 1, vector<int>(l2 + 1, 0));
        
        for(int i = l1 - 1; i >= 0; --i) {
            for(int j = l2 - 1; j >= 0; --j) {
                if(text1[i] == text2[j]) {
                    dp[i][j] = 1 + dp[i + 1][j + 1];
                } else {
                    dp[i][j] = max(dp[i + 1][j], dp[i][j + 1]);
                }
            }
        }
        
        return dp[0][0];
    }
};
```

# Problem Links
https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/lcs-official/ojquestion  
https://leetcode.com/problems/longest-common-subsequence/