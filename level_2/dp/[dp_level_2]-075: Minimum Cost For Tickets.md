# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=YNe1fsHgEOI&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=75)

# Thought Process

Recursive:
- If we choose to buy a `1-day` ticket today, we will spend (`1-day` + `min_cost_of_remaining_days`)
- If we choose to buy a `7-day` ticket today, we will spend (`7-day` + `min_cost_of_remaining_days`)
- If we choose to buy a `30-day` ticket today, we will spend (`30-day` + `min_cost_of_remaining_days`)

# Code

Recursive without memo:

```cpp
class Solution {
    vector<int> days, cost;

    int helper(int idx) {
        if(idx >= days.size()) return 0;

        int cost_day = cost[0] + helper(idx + 1);

        int d = idx;

        while(d < days.size() && days[d] < days[idx] + 7) {
            d++;
        }
        int cost_week = cost[1] + helper(d);

        while(d < days.size() && days[d] < days[idx] + 30) {
            d++;
        }
        int cost_month = cost[2] + helper(d);

        return min({cost_day, cost_week, cost_month});
    }
public:
    int mincostTickets(vector<int>& days, vector<int>& costs) {
        this->days = days, this->cost = costs;
        return helper(0);
    }
};
```

# Problem Links
- https://leetcode.com/problems/minimum-cost-for-tickets/
