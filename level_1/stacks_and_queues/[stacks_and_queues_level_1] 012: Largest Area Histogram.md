# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/141291454-377aa6d2-075a-40c4-905d-0d085e06413c.png)

[Tutorial](https://www.youtube.com/watch?v=0do2734xhnU&list=PL-Jc9J83PIiEyUGT3S8zPdTMYojwZPLUM&index=13)

# Thought Process

- This question uses ideas from: `Find next greater element on left & Stock Span`. Revising them may be helpful, tho they are basic

# Code
```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int n = heights.size();
        stack<int> s;

        // find next smaller on right, for each index
        vector<int> nextSmaller(n);
        for(int i = n - 1; i >= 0; --i) {
            while(!s.empty() && heights[s.top()] >= heights[i])
                s.pop();

            if(s.empty()) nextSmaller[i] = n;
            else nextSmaller[i] = s.top();

            s.push(i);
        }

        s = stack<int>();
        // find next smaller on left, for each index
        vector<int> prevSmaller(n);
        for(int i = 0; i < n; ++i) {
            while(!s.empty() && heights[s.top()] >= heights[i])
                s.pop();

            if(s.empty()) prevSmaller[i] = -1;
            else prevSmaller[i] = s.top();

            s.push(i);
        }

        int ans = 0;
        for(int i = 0; i < n; ++i) {
            ans = max(ans, (nextSmaller[i] - prevSmaller[i] - 1) * heights[i]);
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/largest-rectangle-in-histogram/
