# Problem Statement
Given a list of non-negative integers nums, arrange them such that they form the largest number.

Note: The result may be very large, so you need to return a string instead of an integer.

[Tutorial](https://www.youtube.com/watch?v=VV_KPrG_PzE&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=39)

# Thought Process
- Solution is simple and straightforward
- Code is nice, take a look. Specially the comparator

# Code
```cpp
class Solution {
public:
    string largestNumber(vector<int>& nums) {
        vector<string> numstrings;
        for(auto i: nums) {
            numstrings.push_back(to_string(i));
        }
        sort(numstrings.begin(), numstrings.end(), [](string &s1, string &s2){ return s1+s2>s2+s1; });
        string ans = "";

        for(auto i: numstrings) {
            ans += i;
        }

        while(ans[0]=='0' && ans.length()>1)
            ans.erase(0,1);

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/largest-number/