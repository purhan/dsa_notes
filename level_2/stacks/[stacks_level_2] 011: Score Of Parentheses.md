# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=rWsv46ME6lI&list=PL-Jc9J83PIiE1_SifBEWRsD-fzxrvkja9&index=11)

# Thought Process
- Just implementation

# Code
```cpp
class Solution {
public:
    int scoreOfParentheses(string s) {
        int n = s.length(), ans = 0;
        stack<string> st;
        for(int i = 0; i < n; ++i) {
            string ch = string(1, s[i]);
            if(ch == ")") {
                if(st.top() == "(") {
                    st.pop();
                    st.push("1");
                } else {
                    int score = 0;
                    while(st.top() != "(") {
                        score += stoi(st.top());
                        st.pop();
                    }
                    st.pop();
                    score *= 2;
                    st.push(to_string(score));
                }
            } else {
                st.push(ch);
            }
        }
        while(!st.empty()) {
            ans += stoi(st.top());
            st.pop();
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/score-of-parentheses/
