# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=Cp22SGFpDb8&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=76)

# Thought Process

Recursive:
- Similar to LCS, except we count all the remaining characters in the base condition (instead of returning 0)
- Two pointers on both strings
- If both characters equal, we dont need to delete any of them, so just continue to next chars
- If unequal, we can delete one of the two, or both. Check subproblem in all three cases

# Code

Recursive:
```cpp
class Solution {
    string s1, s2;
    int dp[1005][1005];

    int _ascii(char ch) {
        return int(ch);
    }

    int helper(int i, int j) {
        if(i >= s1.length()) {
            int cost = 0;
            while(j < s2.length()) {
                cost += _ascii(s2[j]);
                ++j;
            }
            return cost;
        }
        if(j >= s2.length()) {
            int cost = 0;
            while(i < s1.length()) {
                cost += _ascii(s1[i]);
                ++i;
            }
            return cost;
        }

        if(dp[i][j] != -1) return dp[i][j];

        if(s1[i] == s2[j]) {
            return dp[i][j] = helper(i + 1, j + 1);
        } else {
            int rem_s1 =  _ascii(s1[i]) + helper(i + 1, j);
            int rem_s2 = _ascii(s2[j]) + helper(i, j + 1);
            int rem_both = _ascii(s1[i]) + _ascii(s2[j]) + helper(i + 1, j + 1);
            return dp[i][j] = min({rem_s1, rem_s2, rem_both});
        }
    }
public:
    int minimumDeleteSum(string s1, string s2) {
        memset(this->dp, -1, sizeof(this->dp));
        this->s1 = s1, this->s2 = s2;
        return helper(0, 0);
    }
};
```

# Problem Links
- https://leetcode.com/problems/minimum-ascii-delete-sum-for-two-strings/
