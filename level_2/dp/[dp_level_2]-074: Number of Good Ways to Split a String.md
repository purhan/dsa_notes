# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=WOPCFFyHxc4&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=74)

# Thought Process
- Not even DP
- For each point, store distinct characters on left, and distinct characters on right in 2 separate maps
- If both values are equal at a point, increment ans

# Code
```cpp
class Solution {
public:
    int numSplits(string s) {
        int n = s.length();
        unordered_map<char, int> freq;
        vector<int> distinctLeft(n, 0), distinctRight(n, 0);
        for(int i = 0; i < n; ++i) {
            if(i > 0) distinctLeft[i] = distinctLeft[i - 1];
            if(freq[s[i]] == 0) distinctLeft[i]++;
            freq[s[i]]++;
        }
        freq.clear();
        for(int i = n - 1; i >= 0; --i) {
            if(i < n - 1) distinctRight[i] = distinctRight[i + 1];
            if(freq[s[i]] == 0) distinctRight[i]++;
            freq[s[i]]++;
        }

        int ans = 0;
        for(int i = 0; i < n - 1; ++i) {
            if(distinctLeft[i] == distinctRight[i + 1]) ans++;
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/number-of-good-ways-to-split-a-string
