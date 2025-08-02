# Problem Statement
1. You are given a number N representing number of elements.
2. You are given N space separated numbers (ELE : elements).
3. Your task is to find & print  
    3.1) "MINIMUM JUMPS" need from 0th step to (n-1)th step.
    3.2) all configurations of "MINIMUM JUMPS".

[Tutorial](https://www.youtube.com/watch?v=phgjL7SbsWs&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=9)

# Thought Process
- Create a 1D DP
- Each cell stores the **minimum jumps from that cell to reach the destination**
- To travel and solve:
  - Traverse the DP from right to left
  - The rightmost cell (or destination) is zero
  - For each cell, we check minimum jumps in all cells from `value[i]` upto `n` and take their minimum


# Code
> :warning: This solution is incomplete, this is for another question
```cpp
class Solution {
public:
    int jump(vector<int>& nums) {
        int n = size(nums);
        vector<int> dp(n, INT_MAX);
        dp[n - 1] = 0;
        
        for(int i = n - 2; i >= 0; --i) {
            for(int j = i + 1; j <= min(n - 1, i + nums[i]); ++j) {
                dp[i] = min(dp[i], dp[j]);
            }
            if(dp[i] != INT_MAX) dp[i]++;
        }
        
        return dp[0];
    }
};
```

# Problem Links
https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/min-jumps-re-official/ojquestion  
https://leetcode.com/problems/jump-game-ii/