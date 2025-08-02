# Problem Statement
1. You are given a number N.
2. You have to find the minimum number of squares that sum to N.
3. You can always represent a number as a sum of squares of other numbers.

For eg - In worst case N can be represented as (1\*1) + (1\*1) + (1\*1)..... N times.

[Tutorial](https://www.youtube.com/watch?v=aZuQXkO0-XA&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=14)

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/134677005-179dd24c-a10b-4c35-a36a-95d97f99c551.png)

- Extremely similar to LIS
- Create a 1D DP
- Each cell stores minimum number of squares that add up to that number

> **Alternative approach:** Coin Change DP. Number can be constructed with minimum coins of value (1, 4, 9, 16, 25...)

# Code
```cpp
class Solution {
public:
    int numSquares(int n) {
        vector<int> dp(n + 1, INT_MAX);
        dp[0] = 0;
        dp[1] = 1;

        for (int i = 2; i <= n; ++i) {
            // Check previous (i - j^2) cell, we can add (j^2) to it. Take minimum of all such options
            for (int j = 1; j * j <= i; ++j) {
                dp[i] = min(dp[i], dp[i - (j * j)]);
            }
            dp[i]++;
        }

        return dp[n];
    }
};
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/min-squares-official/ojquestion
- https://leetcode.com/problems/perfect-squares/
