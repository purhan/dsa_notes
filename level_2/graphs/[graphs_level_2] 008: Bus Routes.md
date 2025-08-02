# Problem Statement

You are given an array routes representing bus routes where routes[i] is a bus route that the ith bus repeats forever.

    For example, if routes[0] = [1, 5, 7], this means that the 0th bus travels in the sequence 1 -> 5 -> 7 -> 1 -> 5 -> 7 -> 1 -> ... forever.

You will start at the bus stop source (You are not on any bus initially), and you want to go to the bus stop target. You can travel between bus stops by buses only.

Return the least number of buses you must take to travel from source to target. Return -1 if it is not possible.

[Tutorial](https://www.youtube.com/watch?v=WhuiqhMXhxM&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=9)

# Thought Process
- For each bus, we are already given what stops you can reach from that bus
- For each stop, we will store what buses you can take from that stop, in a map
- Starting from source stop, we will BFS. We will check what buses we can take and what stops those buses take us to
- Level of BFS, at which we reach target stop, is the ans

# Code
```cpp
class Solution {
public:
    int numBusesToDestination(vector<vector<int>>& routes, int source, int target) {
        int n = size(routes);

        // mp represents: what buses can you take from stop `x`?
        map<int, vector<int>> mp;

        for(int i = 0; i < n; ++i) {
            for(int j = 0; j < size(routes[i]); ++j) {
                int busStop = routes[i][j];
                mp[busStop].push_back(i);
            }
        }

        unordered_map<int, int> bus_visited;
        unordered_map<int, int> stop_visited;
        queue<int> q;

        q.push(source);

        // simple BFS
        int level = 0;
        while(!q.empty()) {
            int level_size = size(q);

            while(level_size--) {
                auto curr_stop = q.front();
                q.pop();

                if(curr_stop == target) {
                    return level;
                }

                for(auto bus: mp[curr_stop]) {
                    if(bus_visited[bus]) continue;

                    bus_visited[bus] = true;
                    for(auto stop: routes[bus]) {
                        if(stop_visited[stop]) continue;

                        q.push(stop);
                        stop_visited[stop] = true;
                    }
                }
            }

            level++;
        }

        return -1;
    }
};
```

# Problem Links
- https://leetcode.com/problems/bus-routes/
