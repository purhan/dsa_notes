# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/140044855-3ece7320-0688-4a21-8960-7c294f7ee1f9.png)

![image](https://user-images.githubusercontent.com/10897423/140044924-330f6c5a-7f30-401c-b4c5-d92cd3263095.png)

[Tutorial](https://www.youtube.com/watch?v=Z9o-lqwgSWA&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=75)

# Thought Process
- Sort by ending points
- For each balloon, till this balloon ends, no other balloon is ending, but only some are starting. We can burst all these balloons with one single arrow
- For the next balloon, if it's starting point lies before previous balloon's ending point, this one is already counted so we skip
- For the next balloon, if it's starting point lies after previous balloon's ending point, we update our lastEndingIndex and continue this process

# Code
```cpp
class Solution {
    static bool comp(const vector<int>& a, vector<int>& b) {
        return a[1] < b[1];
    }
public:
    int findMinArrowShots(vector<vector<int>>& points) {

        // sort by ascending ENDING points of balloons
        sort(points.begin(), points.end(), comp);
        int ans = 1, end = points[0][1];

        // if some balloon starts AFTER this ends, we need another arrow for it
        for(int i = 1; i < points.size(); ++i) {
            if(points[i][0] > end) {
                ans++;
                end = max(end, points[i][1]);
            }
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/
