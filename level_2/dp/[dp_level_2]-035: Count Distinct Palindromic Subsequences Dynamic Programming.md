# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=fvYlinirmFg&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=37)

# Thought Process

Follow up: Do recursively

![image](https://user-images.githubusercontent.com/10897423/150808559-40c95828-8028-4980-bd60-1ce4f62497b4.png)

![image](https://user-images.githubusercontent.com/10897423/150810597-e0aae484-5f48-4b5d-bd16-9fadcb106113.png)

- To solve iteratively, we will use gap strategy
- There can be 2 scenarios mainly:
  - s[i] != s[j]
    - In that case, we just count palindromes in `i+mid` and `mid+j` (and subtract mid because we counted it twice)
  - s[i] == s[j] (calling it ch): Now, there can be 3 scenarios:
    - ch is not present between i and j:
      - `res = 2 * mid + 2`
    - ch is present once
      - `res = 2 * mid + 1`
    - ch is present twice or more (we don't care more than 2 because that'll be taken care of recursively)
      - `res = 2 * mid - res_ch1_ch2`

# Code
```cpp
class Solution {
public:
    int countPalindromicSubsequences(string s) {
        int n = s.length();
        vector<vector<long long>> dp(n + 1, vector<long long>(n + 1));

        map<char, int> mp;
        vector<int> prev(n), next(n);
        for(int i = 0; i < n; ++i) {
            char ch = s[i];
            if(mp.count(ch) == 0) {
                prev[i] = -1;
            } else {
                prev[i] = mp[ch];
            }
            mp[ch] = i;
        }
        mp = map<char, int>();
        for(int i = n - 1; i >= 0; --i) {
            char ch = s[i];
            if(mp.count(ch) == 0) {
                next[i] = -1;
            } else {
                next[i] = mp[ch];
            }
            mp[ch] = i;
        }

        for(int g = 0; g < n; ++g) {
            for(int i = 0, j = g; j < n; ++i, ++j) {
                if(g == 0) {
                    dp[i][j] = 1;
                } else if(g == 1) {
                    dp[i][j] = 2;
                } else {
                    if(s[i] != s[j]) {
                        dp[i][j] = dp[i + 1][j] + dp[i][j - 1] - dp[i + 1][j - 1];
                    } else {
                        int N = next[i];  // next index starting
                        int P = prev[j];  // previous index of ending

                        if(N > P) {
                            dp[i][j] = 2 * dp[i + 1][j - 1] + 2;
                        } else if(N == P) {
                            dp[i][j] = 2 * dp[i + 1][j - 1] + 1;
                        } else {
                            dp[i][j] = 2 * dp[i + 1][j - 1] - dp[N + 1][P - 1];
                        }
                    }
                }
            }
        }
        return dp[0][n - 1];
    }
};
```

# Problem Links
- https://leetcode.com/problems/count-different-palindromic-subsequences/