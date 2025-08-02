# Problem Statement
1. A conveyor belt has packages that must be shipped from one port to another within D days.
2. The ith package on the conveyor belt has a weight of weights[i]. Each day, we load the ship with packages on the conveyor belt (in the order given by weights). We may not load more weight than the maximum weight capacity of the ship.
3. Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within D days.

[Tutorial](https://www.youtube.com/watch?v=eq6dAJefOqc&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=24)

# Thought Process
- Same as Allocate Minimum Number of Books problem and Split Array Largest Sum problem

> Leetcode's hint: Binary search on the answer. We need a function possible(capacity) which returns true if and only if we can do the task in D days.

# Code
```cpp
class Solution {
    bool isPossible(vector<int> weights, int days, int mid) {
        int cnt = 1, sum = 0;

        for(int i = 0; i < weights.size(); ++i) {
            sum += weights[i];
            if(sum > mid) {
                cnt++;
                sum = weights[i];
            }
        }

        return cnt <= days;
    }
public:
    int shipWithinDays(vector<int>& weights, int days) {
        int ans = 0;
        int lo = *max_element(weights.begin(), weights.end());
        int hi = accumulate(weights.begin(), weights.end(), 0);

        while(lo <= hi) {
            int mid = lo + (hi - lo) / 2;

            if(isPossible(weights, days, mid)) {
                ans = mid;
                hi = mid - 1;
            } else {
                lo = mid + 1;
            }
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/capacity_to_ship_within_d_days/ojquestion
