# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/144809882-6c25f285-7032-4360-9333-086d5264f1ba.png)

[Tutorial](https://www.youtube.com/watch?v=XjLT4TaXsgw&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=64)

Difference from Arithmetic Slices 1: Here the sequences are not contiguous

# Thought Process
- 2D DP, each cell stores: Number of Arithmetic slices here of `[common difference][length]`
- For each cell, check all previous numbers and all common differences, like we do in LIS. Update the same for this number and increment the answer accordingly

# Code
```cpp
class Solution {
public:
    int numberOfArithmeticSlices(vector<int>& nums) {
        int n = nums.size(), ans = 0;
        vector<unordered_map<long long, int>> dp(n);

        for(int i = 1; i < n; ++i) {
            for(int j = 0; j < i; ++j) {
                long long diff = (long long)nums[i] - nums[j];
                int cnt = dp[j].count(diff) ? dp[j][diff] : 0;
                dp[i][diff] += cnt + 1;
                ans += cnt;
            }
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/arithmetic-slices-ii-subsequence/
