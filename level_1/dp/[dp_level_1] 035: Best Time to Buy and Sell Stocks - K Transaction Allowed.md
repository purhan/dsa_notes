# Problem Statement

You are given an integer array prices where prices[i] is the price of a given stock on the ith day, and an integer k.

Find the maximum profit you can achieve. You may complete at most k transactions.

Note: You may not engage in multiple transactions simultaneously (i.e., you must sell the stock before you buy again).

[Tutorial](https://www.youtube.com/watch?v=3YILP-PdEJA&list=PL-Jc9J83PIiG8fE6rj9F5a6uyQ5WPdqKy&index=36)

# Thought Process
- Ponder over a recursive solution too!
- For bottom-up, this is what we do:
- We create a 2D Dp, each cell tells us -> Maximum profit on that day, if _row_ transactions are allowed in _column_ days

# Code
```cpp
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        int n = size(prices);
        if(n == 0) return 0;
        vector<vector<int>> dp(n + 1, vector<int>(n + 1, 0));

        for(int t = 1; t <= k; ++t) {
            for(int d = 1; d < n; ++d) {
                dp[t][d] = max(dp[t][d], dp[t][d - 1]);

                for(int i = 0; i < d; ++i) {
                    dp[t][d] = max(dp[t][d], prices[d] - prices[i] + dp[t - 1][i]);
                }
            }
        }

        return dp[k][n - 1];
    }
};
```

# Problem Links
- https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/
