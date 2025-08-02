# Problem Statement
1. You are given an array(arr) of length N which represents N number of balloons.
2. Each balloon is painted with a number on it.
3. You have to collect maximum coins by bursting all the balloons.
4. If you burst a balloon with index i, you will get (arr[i-1] * arr[i] * arr[i+1]) number of coins.
5. If arr[i-1] and arr[i+1] don't exist, then you may assume their value as 1.

[Tutorial](https://www.youtube.com/watch?v=YzvF8CqPafI&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=24)

> :warning::warning::warning: This one needs strong revision :warning::warning::warning:

# Thought Process
- Derivative of MCM
- Watch tutorial for clarity

# Code
```cpp
class Solution {
public:
    int maxCoins(vector<int>& nums) {
        int n = size(nums);
        vector<vector<int>> dp(n, vector<int>(n, 0));

        for(int g = 0; g < n; ++g) {
            for(int i = 0, j = g; j < n; ++i, ++j) {
                for(int k = i; k <= j; ++k) {
                    int left = ((k == i) ? 0 : dp[i][k - 1]);
                    int right = ((k == j) ? 0 : dp[k + 1][j]);
                    int val = ((i == 0) ? 1 : nums[i - 1]) * nums[k] * ((j == n - 1) ? 1 : nums[j + 1]);

                    dp[i][j] = max(dp[i][j], left + right + val);
                }
            }
        }

        return dp[0][n - 1];
    }
};
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/burst-balloons-official/ojquestion#!
- https://leetcode.com/problems/burst-balloons/submissions/
