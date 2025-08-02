# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/147383041-77a1a5a6-fe6f-41ea-809b-be956f2c137d.png)

[Tutorial](https://www.youtube.com/watch?v=bgWt2qtFhbQ&list=PL-Jc9J83PIiE1_SifBEWRsD-fzxrvkja9&index=17)

# Thought Process
- Use code from LC 84 (previous question)
- Maximal rectangle is the largest histogram out of all rows

![image](https://user-images.githubusercontent.com/10897423/147383072-a4361a67-95de-4c65-89f9-73c341a12289.png)

# Code
```cpp
class Solution {
public:
    int maximalRectangle(vector<vector<char>>& matrix) {
        int ans = 0;
        vector<int> heights(matrix[0].size(), 0);

        for(int i = 0; i < matrix.size(); ++i) {
            for(int j = 0; j < matrix[i].size(); ++j) {
                if(matrix[i][j] == '0') {
                    heights[j] = 0;
                } else {
                    heights[j]++;
                }
            }
            ans = max(ans, largestRectangleArea(heights));
        }
        return ans;
    }

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
- https://leetcode.com/problems/maximal-rectangle/
