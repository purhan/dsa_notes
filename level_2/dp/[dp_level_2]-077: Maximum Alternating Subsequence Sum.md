# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=GXMxCGnqdKE&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=77)

# Thought Process

Recursive:
- A number can be chosen or skipped
- Moreover, if chosen, it can be at even index or odd index

# Code

Recursive:
```cpp
class Solution {
    vector<int> nums;

    long long helper(int idx, int sz) { // {idx of cur element, size of array (whether even or odd)}
        if(idx >= nums.size()) return 0;

        int chosen = 0;
        if(sz % 2) {
            chosen = helper(idx + 1, 0) + nums[idx];
        } else {
            chosen = helper(idx + 1, 1) - nums[idx];
        }

        int skipped = helper(idx + 1, sz);

        return max(skipped, chosen);
    }
public:
    long long maxAlternatingSum(vector<int>& nums) {
        this->nums = nums;
        return helper(0, 1);
    }
};
```

Memoized:
```cpp
class Solution {
    vector<int> nums;
    vector<vector<long long int>>dp;

    long long helper(int idx, int chance) { // {idx of cur element, chance (whether even or odd)}
        if(idx == nums.size()) return 0;

        if(dp[idx][chance] != -1) return dp[idx][chance];

        long long chosen = 0, skipped = 0;
        if(chance == 1) {
            chosen = helper(idx + 1, 0) + nums[idx];
            skipped = helper(idx + 1, chance);
            return dp[idx][chance] = max(chosen, skipped);
        } else {
            chosen = helper(idx + 1, 1) - nums[idx];
            skipped = helper(idx + 1, chance);
            return dp[idx][chance] = max(chosen, skipped);
        }
    }
public:
    long long maxAlternatingSum(vector<int>& nums) {
        this->nums = nums;
        this->dp = vector<vector<long long int>>(nums.size()+2,vector<long long int>(2,-1));
        return helper(0, 1);
    }
};
```

# Problem Links
- https://leetcode.com/problems/maximum-alternating-subsequence-sum/
