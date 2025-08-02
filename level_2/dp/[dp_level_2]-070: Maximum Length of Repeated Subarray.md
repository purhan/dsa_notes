# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=Zg3HBicw4LU&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=70)

# Thought Process
- Exactly same as longest common substring (contiguous)

# Code
```cpp
class Solution {
public:
    int findLength(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size();
        int m = nums2.size();
        vector<vector<int>> dp(n, vector<int>(m));
        int ans = 0;

        for(int i = 0; i < n; ++i) {
            for(int j = 0; j < m; ++j) {
                if(i == 0 || j == 0) {
                    dp[i][j] = (nums1[i] == nums2[j]);
                } else {
                    if(nums1[i] == nums2[j]) {
                        dp[i][j] = dp[i - 1][j - 1] + 1;
                    }
                }
                ans = max(ans, dp[i][j]);
            }
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/maximum-length-of-repeated-subarray/
