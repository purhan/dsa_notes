# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=WrFbV00pGSc&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=72)

# Thought Process
- We are only allowed to cut at certain points, given in an array `cuts`
- For each point, recursively check `cost[left, this_pt] + cost[this_pt, right] + length_of_stick`

# Code
```cpp
class Solution {
    vector<int> cuts;
    int dp[102][102] ={};

    int helper(int l, int r) {
        if(l + 1 == r) return 0;

        if(dp[l][r] != 0) return dp[l][r];

        int mn = INT_MAX;
        int length_of_stick = cuts[r] - cuts[l];
        for(int i = l + 1; i < r; ++i) {
            mn = min(mn, length_of_stick + helper(l, i) + helper(i, r));
        }
        return dp[l][r] = mn;
    }
public:
    int minCost(int n, vector<int>& cuts) {
        cuts.push_back(0);
        cuts.push_back(n);
        sort(cuts.begin(), cuts.end());
        this->cuts = cuts;
        return helper(0, cuts.size() - 1);
    }
};
```

# Problem Links
- https://leetcode.com/problems/minimum-cost-to-cut-a-stick/
