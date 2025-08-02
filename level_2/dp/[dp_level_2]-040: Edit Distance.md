# Problem Statement
1. You are given two strings s1 and s2.
2. You have to find the minimum number of operations needed to convert s1 to s2.
```
   Operations allowed are -
   Insert - You can insert any character in s1.
   Remove - You can remove any character in s1.
   Replace - You can replace any character in s1 with any other character.
```

[Tutorial](https://www.youtube.com/watch?v=tooMn-xfYCU&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=40)

# Thought Process
- We need a 2D DP table
- On 0'th row and 0'th column, the values are 0, 1, 2 ... so on. The reason: The minimum cost to make the string equal to _blank_ is just it's length
- Look at the screenshot for the other cells

![image](https://user-images.githubusercontent.com/10897423/135049391-22d5d005-ce06-4891-ae07-3bf51729cf73.png)

- When deleting, length of s1 will decrease, so we just look at previous row
- When inserting, length of s1 will increase and relatively s2 will decrease, so we look at previous column
- When replacing, we look at previous diagonal cell

From CP Handbook:

![image](https://user-images.githubusercontent.com/10897423/135066075-7074f407-561c-4498-bc13-5bebd2e05d32.png)


# Code
```cpp
void solve(string s1, string s2, int n, int m) {
    vector<vector<int>> dp(n + 1, vector<int>(m + 1, 0));

    for (int i = 0; i <= n; ++i) {
        for (int j = 0; j <= m; ++j) {
            if (i == 0) {
                dp[i][j] = j;
            } else if (j == 0) {
                dp[i][j] = i;
            } else {
                if (s1[i - 1] == s2[j - 1]) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else  {
                    int factor1 = 1 + dp[i - 1][j - 1]; // if replaced
                    int factor2 = 1 + dp[i - 1][j]; // if deleted
                    int factor3 = 1 + dp[i][j - 1]; // if inserted
                    dp[i][j] = min({factor1, factor2, factor3});
                }
            }
        }
    }

    cout << dp[n][m];
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/edit-distance-official/ojquestion#!
- https://leetcode.com/problems/edit-distance/
