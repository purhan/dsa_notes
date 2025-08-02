# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/144644993-4a1105b5-4fce-48de-813d-8a6cfa40d1ce.png)

[Tutorial](https://www.youtube.com/watch?v=VOWpn_bWS0U&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=54)

# Thought Process

Recursive:
- For each character of source string, if that character doesn't match the first char of target, we HAVE to drop it
- If it matches, we can either drop it, or keep it. If we keep it, only the remaining target string has to be checked. This diagram may explain better

![image](https://user-images.githubusercontent.com/10897423/144645591-b5647ed1-3f14-4f96-b291-8aeae5079a98.png)

- We are only comparing first chars of source and target. If they don't match we drop first char of source. If they match, we aither drop c1, or we drop both c1 and c2.

`Tutorial also explained tabulation`

# Code
```cpp
class Solution {
    vector<vector<int>> dp;

    int helper(string& s, string& t, int si, int ti) {
        if(si >= s.length()) {
            if(ti < t.length()) return 0;
            else return 1;
        } else if(ti >= t.length())
            return 1;

        if(dp[si][ti] != -1) return dp[si][ti];

        if(s[si] != t[ti]) {
            return dp[si][ti] = helper(s, t, si + 1, ti);
        } else {
            int inc = helper(s, t, si + 1, ti + 1);
            int exc = helper(s, t, si + 1, ti);
            return dp[si][ti] = inc + exc;
        }
    }
public:
    int numDistinct(string s, string t) {
        dp = vector<vector<int>>(s.length() + 1, vector<int>(t.length(), -1));
        return helper(s, t, 0, 0);
    }
};
```

# Problem Links
- https://leetcode.com/problems/distinct-subsequences/
