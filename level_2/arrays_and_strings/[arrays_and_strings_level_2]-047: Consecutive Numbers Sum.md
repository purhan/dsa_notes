# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=EiC2eIlYu_w&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=47)

# Thought Process

MUST REVISE!!! MATH, NOT CLEAR

# Code

```cpp
class Solution {
    string encode(string s) {
        string code = s;
        unordered_map<char, int> assignedToken;

        int curToken = '1';
        for(int i = 0; i < s.length(); ++i) {
            if(assignedToken[s[i]]) {
                s[i] = assignedToken[s[i]];
            } else {
                assignedToken[s[i]] = curToken;
                curToken += 1;
                s[i] = assignedToken[s[i]];
            }
        }
        return s;
    }
public:
    vector<string> findAndReplacePattern(vector<string>& words, string pattern) {
        vector<string> ans;

        string p = encode(pattern);
        for(auto w: words) {
            if(encode(w) == p) ans.push_back(w);
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/consecutive-numbers-sum/
