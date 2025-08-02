# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=RCE2L0Zk7xE&list=PL-Jc9J83PIiE1_SifBEWRsD-fzxrvkja9&index=20)

# Thought Process
- It is greedily best to remove the first index for which `s[i] > s[i + 1]` since `i` is a more significant digit than `i + 1`

# Code
```cpp
class Solution {
public:
    string removeKdigits(string num, int k) {
        stack<char> st;

        for(int i = 0; i < num.length(); ++i) {
            char ch = num[i];

            while(!st.empty() && k > 0 && st.top() > ch) {
                st.pop();
                k--;
            }
            st.push(ch);
        }

        while(k > 0) {
            st.pop();
            k--;
        }

        string ans = "";
        while(!st.empty()) {
            ans += st.top();
            st.pop();
        }
        while(ans.back() == '0') ans.pop_back();
        if(ans == "") ans = "0";
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/remove-k-digits/
