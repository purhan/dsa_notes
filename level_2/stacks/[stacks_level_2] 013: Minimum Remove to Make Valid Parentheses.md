# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=Givpwgu9IIc&list=PL-Jc9J83PIiE1_SifBEWRsD-fzxrvkja9&index=13)

# Thought Process
- Just implementation

# Code
```cpp
class Solution {
public:
    string minRemoveToMakeValid(string s) {
      stack<int> st;
      for (auto i = 0; i < s.size(); ++i) {
        if (s[i] == '(') st.push(i);
        if (s[i] == ')') {
          if (!st.empty()) st.pop();
          else s[i] = '*';
        }
      }
      while (!st.empty()) {
        s[st.top()] = '*';
        st.pop();
      }
      s.erase(remove(s.begin(), s.end(), '*'), s.end());
      return s;
    }
};
```

# Problem Links
- https://leetcode.com/problems/minimum-remove-to-make-valid-parentheses/
