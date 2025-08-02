# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/139694796-9e4edf15-a18b-4226-935b-4359f9534b58.png)

[Tutorial](https://www.youtube.com/watch?v=fmdNUOQnhrU&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=73)

# Thought Process
- We use 2 pointers on each list
- Whichever list's current ending point is smaller, we move that pointer
- We take `[common starting point, common ending point]` everytime

# Code
```cpp
class Solution {
public:
    vector<vector<int>> intervalIntersection(vector<vector<int>>& firstList, vector<vector<int>>& secondList) {
        int n = firstList.size();
        int m = secondList.size();
        int ptr1 = 0, ptr2 = 0;
        vector<vector<int>> ans;

        while(ptr1 < n && ptr2 < m) {
            int commonSP = max(firstList[ptr1][0], secondList[ptr2][0]);
            int commonEP = min(firstList[ptr1][1], secondList[ptr2][1]);

            if(commonSP <= commonEP) {
                vector<int> interval = {commonSP, commonEP};
                    ans.push_back(interval);
            }

            if(firstList[ptr1][1] < secondList[ptr2][1]) ptr1++;
            else ptr2++;
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/interval-list-intersections/
