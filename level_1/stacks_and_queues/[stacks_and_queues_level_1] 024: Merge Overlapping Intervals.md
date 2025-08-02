# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/139541176-6a05bbd1-6d27-4f43-8b60-77963c921448.png)

[Tutorial](https://www.youtube.com/watch?v=QlaDyZTCAbM&list=PL-Jc9J83PIiEyUGT3S8zPdTMYojwZPLUM&index=24)

# Thought Process
- Sort by starting point
- If current interval is starting before last interval of the stack finished, these two will get merged. So just update the top of the stack
- Lastly, stack will be the ans

# Code
```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        int n = intervals.size();
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> ans;

        stack<vector<int>> s;
        for(int i = 0; i < n; ++i) {
            if(s.empty() || s.top()[1] < intervals[i][0]) s.push(intervals[i]);
            else {
                vector<int> t = s.top(); s.pop();
                t[1] = max(t[1], intervals[i][1]);
                s.push(t);
            }
        }

        while(!s.empty()) {
            ans.push_back(s.top());
            s.pop();
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/merge-intervals/
