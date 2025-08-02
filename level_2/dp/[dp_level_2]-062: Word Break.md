# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/144817216-1ee71d65-a17e-4a53-ab38-a485507b6701.png)

[Tutorial](https://www.youtube.com/watch?v=2NaaM_z_Jig&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=62)

ALthough on portal they say word-break-2, this tutorial only explains word-break-1

# Thought Process

Recursive:
- For each index in string, take prefix string till that index. If this prefix exists in dict, check for remaining string, if that is also true then answer is true
- Memoize only the index at which we are checking since only that is changing everytime

Iterative (explained in tutorial):
- Same idea as recursive

# Code

Recursive (done by me)

```cpp
class Solution {
    map<string, bool> dictContains;
    string s;
    vector<int> dp;

    bool helper(int j) {
        if(j == s.length()) return true;
        if(dp[j] != -1) return dp[j];

        bool res = false;

        for(int i = 1; i < s.length() - j + 1; ++i) {
            string prefix = s.substr(j, i);
            if(dictContains[prefix])
                res = res || helper(j + i);
        }
        return dp[j] = res;
    }
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        for(auto word: wordDict) {
            this->dictContains[word] = true;
        }
        this->s = s;
        this->dp = vector<int>(s.length() + 1, -1);
        return helper(0);
    }
};
```

# Problem Links
- https://leetcode.com/problems/word-break/
