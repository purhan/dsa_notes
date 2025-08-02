# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/142200478-e60dacc1-1474-4f4f-aa19-6adf5b5d329d.png)

[Tutorial](https://www.youtube.com/watch?v=jFZmBQ569So&list=PL-Jc9J83PIiG8fE6rj9F5a6uyQ5WPdqKy&index=25)

# Thought Process
- Prepending 0's were handled differently in tutorial as opposed to LC question
- Kinda similar to LIS, in that, at every index, we want the number of decodings. Read the [second] code to understand more

# Code
```cpp
class Solution {
public:
    int numDecodings(string s) {
        int n = s.size();
        vector<int> mem(n + 1, -1);
        mem[n] = 1; 
        return s.empty() ? 0 : num(0, s, mem);   
    }

    int num(int i, string &s, vector<int> &mem) {
        if(mem[i] > -1) 
            return mem[i];
        if(s[i] == '0') 
            return mem[i] = 0;

        int res = num(i + 1, s, mem);

        if(i < s.size() - 1 && (s[i] == '1' || s[i] == '2' && s[i+1] < '7')) {
            res += num(i + 2, s, mem);
        }

        return mem[i] = res;
    }
};
```

Cleaner Code that didnt work on LC
```cpp
class Solution {
public:
    int numDecodings(string s) {
        if(s[0] == '0') return 0;
        int n = size(s);
        vector<int> dp(n + 1, 0);
        dp[0] = 1;

        for(int i = 1; i < n; ++i) {
            if(s[i - 1] == 0 && s[i] == '0') {
                dp[i] = 0;
            } else if(s[i - 1] != 0 && s[i] == '0') {
                if(s[i - 1] == '2' || s[i - 1] == '1') {
                    dp[i] = (i > 1 ? dp[i - 2] : 1);
                } else {
                    dp[i] = 0;
                }
            } else if(s[i - 1] == 0 && s[i] != '0') {
                dp[i] = dp[i - 1];
            } else {
                if(stoi(s.substr(i - 1, i + 1)) <= 26) {
                    dp[i] = dp[i - 1] + (i > 1 ? dp[i - 2] : 1);
                } else {
                    dp[i] = dp[i - 1];
                }
            }
        }

        return dp[n - 1];
    }
};
```

# Problem Links
- https://leetcode.com/problems/decode-ways/
