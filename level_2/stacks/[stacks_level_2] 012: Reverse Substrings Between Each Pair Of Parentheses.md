# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=4a4bspKyOH8&list=PL-Jc9J83PIiE1_SifBEWRsD-fzxrvkja9&index=12)

# Thought Process
- Just implementation

# Code
```cpp
class Solution {
public:
    string reverseParentheses(string s) {
        stack<int> st;
        string res;
        for (int i = 0; i < s.size(); i ++) {
            if (s[i] == '(') {
                st.push(i);
            } else if (s[i] == ')') {
                int top = st.top();
                st.pop();
                reverse(s.begin() + top + 1, s.begin() + i);
            }
        }
        for (auto it: s) {
            if (it != '(' && it != ')') {
                res.push_back(it);
            }
        }
        return res;
    }
};
```

# Problem Links
- https://leetcode.com/problems/reverse-substrings-between-each-pair-of-parentheses/
