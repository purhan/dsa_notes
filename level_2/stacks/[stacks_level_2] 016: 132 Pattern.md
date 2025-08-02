# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=zesp0cWYs4w&list=PL-Jc9J83PIiE1_SifBEWRsD-fzxrvkja9&index=20)

# Thought Process
- Greedily store the minimum value on left of each value
- Use stack to find next greater element than the minSoFar at each index

# Code
```cpp
class Solution {
public:
    bool find132pattern(vector<int>& nums) {
        int n = nums.size();
        vector<int> minSoFar(n);

        minSoFar[0] = nums[0];
        for(int i = 1; i < n; ++i) {
            minSoFar[i] = min(minSoFar[i - 1], nums[i]);
        }

        stack<int> st;
        for(int i = n - 1; i >= 0; --i) {
            while(!st.empty() && st.top() <= minSoFar[i]) st.pop();
            if(!st.empty() && st.top() < nums[i]) {
                return true;
            }
            st.push(nums[i]);
        }
        return false;
    }
};
```

# Problem Links
- https://leetcode.com/problems/132-pattern/
