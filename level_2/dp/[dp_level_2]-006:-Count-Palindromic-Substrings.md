# Problem Statement
1. You are given a string str.
2. You are required to print the count of palindromic substrings in string str.  

[Tutorial](https://www.youtube.com/watch?v=XmSOWnL6T_I&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=6)

> **Note:** Remember to read [Manacher's Algorithm](https://www.geeksforgeeks.org/manachers-algorithm-linear-time-longest-palindromic-substring-part-1/) for better time complexity


# Thought Process

- Create a 2-D DP

![image](https://user-images.githubusercontent.com/10897423/133931781-218b27ee-c060-427d-b104-b8c9b3b29d92.png)

- Each cell represents the **Count of palindromic substrings in a string starting at vertical index and ending at horizontal index**
- A string is a palindrome if:
    - Its length is 1  
    OR  
    - Its first and last characters are same
    - The substring excluding first and last character is also a substring
- For example, to check if `bccb` is a palindrome, we need to check the first and last characters (both same in this case), AND we check the DP state for `cc`

# Code
This particular implementation uses `gap strategy`
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

            if (dp[i][j]) ans++;
        }
    }

    return ans;
}
```

# Problem Links
https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/cps-official/ojquestion