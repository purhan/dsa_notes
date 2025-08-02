# Problem Statement
1. Winter is coming! During the contest, your first job is to design a standard heater with a fixed warm radius to warm all the houses.
2. Every house can be warmed, as long as the house is within the heater's warm radius range.
3. Given the positions of houses and heaters on a horizontal line, return the minimum radius standard of heaters so that those heaters could cover all houses.
4. Notice that all the heaters follow your radius standard, and the warm radius will the same.

[Tutorial](https://www.youtube.com/watch?v=xR2SzAmiUpM&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=37)

# Thought Process
- Sort the `heaters` array, and for each house, find nearest heater for it towards left or towards right
- Return the maximum such heater distance

# Code

This code didn't give AC but its good for understanding a general idea

```cpp
class Solution {
    pair<int, int> binarySearch(int house, vector<int> heaters) {
        int lo = 0, hi = size(heaters) - 1;
        pair<int, int> res = {-1, -1};              // res.first  -> heater just left of house
                                                    // res.second -> heater just right of house
        while(lo <= hi) {
            int mid = (hi + lo) / 2;

            if(heaters[mid] == house) {
                return {heaters[mid], heaters[mid]};
            } else if(heaters[mid] < house) {
                res.first = heaters[mid];
                lo = mid + 1;
            } else {
                res.second = heaters[mid];
                hi = mid - 1;
            }
        }

        return res;
    }

public:
    int findRadius(vector<int>& houses, vector<int>& heaters) {
        sort(heaters.begin(), heaters.end());

        int ans = 0;

        for(auto h: houses) {
            pair<int, int> p = binarySearch(h, heaters);

            int dist_left = (p.first == -1) ? INT_MAX : (h - p.first);
            int dist_right = (p.second == -1) ? INT_MAX : (p.second - h);
            int min_req_distance = min(dist_left, dist_right);
            ans = max(ans, min_req_distance);
        }

        return ans;
    }
};
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/heaters-official/ojquestion
