# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=41VuLYR0btE&list=PL-Jc9J83PIiE1_SifBEWRsD-fzxrvkja9&index=7)

# Thought Process
- Find next smaller on left
- Find next smaller on right
- Using stacks... You know how to (level 1)
- The largest histogram at any index = (min[previous smaller, next smaller] * distance between the two)
- Find largest of all indeces

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
