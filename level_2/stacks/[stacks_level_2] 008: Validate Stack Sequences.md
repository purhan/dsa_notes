# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=KsIeZfmvuVQ&list=PL-Jc9J83PIiE1_SifBEWRsD-fzxrvkja9&index=8)

# Thought Process
- Keep one pointer on `popped`
- Keep pushing next element till we reach the first element to pop
- Keep popping if top element is same as next element to be popped
- If all elements popped in the end, then answer is true, else false

# Code
```cpp
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        stack<int> s;

        int i = 0;
        for(auto p: pushed) {
            s.push(p);
            while(s.size() > 0 && s.top() == popped[i]) {
                s.pop();
                i++;
            }
        }

        if(i == popped.size()) return true;
        return false;
    }
};
```

# Problem Links
- https://leetcode.com/problems/validate-stack-sequences/
