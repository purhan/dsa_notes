# Problem Statement
1. You are given a number n, representing the number of envelopes.
2. You are given n pair of numbers, representing the width and height of each envelope.
3. You are required to print the count of maximum number of envelopes that can be nested inside each other.
Note - Rotation is not allowed.

# Thought Process
- Sort by width
- Apply LIS on height
- Note: Same (equal) width/height cannot be nested, it must be strictly smaller

# Code
```cpp
class Solution {
public:
    int maxEnvelopes(vector<vector<int>>& envelopes) {
        int n = size(envelopes);
        sort(envelopes.begin(), envelopes.end());
        vector<int> dp(n + 1, 0);
        dp[0] = 1;
        
        for(int i = 1; i < n; ++i) {
            for(int j = 0; j < i; ++j) {
                if(envelopes[i][0] > envelopes[j][0] && envelopes[i][1] > envelopes[j][1]) {
                    dp[i] = max(dp[i], dp[j]);
                }
            }
            dp[i]++;
        }
        
        return *max_element(dp.begin(), dp.end());
    }
};
```

# Problem Links
https://leetcode.com/problems/russian-doll-envelopes/