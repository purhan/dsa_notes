# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138735651-3fc2abed-840c-4e52-908d-10bb1057a27c.png)

[Tutorial](https://www.youtube.com/watch?v=QeBvfH1dpOU&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=43)

# Thought Process
- Use map, assign a key to each character and use that as a hash. If a hash matches pattern, add it to ans

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
- https://leetcode.com/problems/find-and-replace-pattern/
