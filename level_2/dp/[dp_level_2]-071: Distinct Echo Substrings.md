# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=UsrW60_lbRs&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=74)

# Thought Process
- Just get all even length substrings and check if they are echoing
- Pay attention to the `string_view` data type for faster comparison. Using string directly will TLE

# Code
```cpp
class Solution {
    bool isEcho(string_view& s) {
        return (s.substr(0, s.length() / 2) == s.substr(s.length() / 2));
    }
public:
    int distinctEchoSubstrings(string text) {
        int n = text.length();
        int ans = 0;
        unordered_set<string_view> s;

        string_view str = text;
        for(int i = 2; i <= n; i += 2) {
            for(int j = 0; j + i <= n; ++j) {
                s.insert(str.substr(j, i));
            }
        }

        for(auto st: s) {
            if(isEcho(st)) ans++;
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/distinct-echo-substrings/
