# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=HUfUzA9Ekgo&list=PL-Jc9J83PIiE1_SifBEWRsD-fzxrvkja9&index=25)

# Thought Process
- Use one stack to store both sign and number
- While you don't encounter a bracket, keep taking numbers, and adding it to the answer according to the signs you get
- Whenever you encounter a closing bracket, In the stack, top 2 items should be -> last calculated value within that bracket pair, and sign of the brackets
- Pop those two and change the answer accordingly

# Code
```cpp
class Solution {
public:
    int calculate(string s) {
        stack <int> st;
        long long num = 0;
        int ans = 0;
        int sign = 1;
        for (char c : s) {
            if (isdigit(c)) {
                num = num * 10 + c - '0';
            } else {
                ans += sign * num;
                num = 0;
                if (c == '+') sign = 1;
                if (c == '-') sign = -1;
                if (c == '(') {
                    st.push(ans);
                    st.push(sign);
                    ans = 0;
                    sign = 1;
                }
                if (c == ')') {
                    ans *= st.top(); st.pop();
                    ans += st.top(); st.pop();
                }
            }
        }
        ans += sign * num;
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/basic-calculator/
