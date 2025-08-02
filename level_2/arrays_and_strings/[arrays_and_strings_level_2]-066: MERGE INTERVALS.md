# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/139541176-6a05bbd1-6d27-4f43-8b60-77963c921448.png)

[Tutorial](https://www.youtube.com/watch?v=_FkR5zMwHQ0&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=66)

# Thought Process

> Same question is solved in stack level 1

- Sort on the basis of starting time of an interval
- Create an answer array
- Insert the first interval in answer
- For every next interval, there are 2 possibillities:
    - It goes outside the end of last interval (in this case, this gets added to answer directly)
    - It stays inside, or on same index as the ending of the last interval (In this case, we update the last interval's ending time only, and move on)

# Code
```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        int n = intervals.size();
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> ans;

        for(int i = 0; i < n; ++i) {
            if(i > 0) {
                if(intervals[i][0] <= ans.back()[1]) {
                    ans.back()[1] = max(ans.back()[1], intervals[i][1]);
                    continue;
                }
            }

            ans.push_back(vector<int>({intervals[i][0], intervals[i][1]}));
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/merge-intervals/
