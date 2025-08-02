# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/142736521-587ec7a2-b076-4417-9d4b-dec4b55db932.png)

![image](https://user-images.githubusercontent.com/10897423/142736531-9b615f48-5aae-448d-bf3a-f94f62b5e577.png)

[Tutorial](https://www.youtube.com/watch?v=Wq1NibUMrNU&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=17)

# Thought Process

Please revise this by coding again from scratch

- Simple implementation of dijkstra. For each path, the MAXIMUM point on that path is the cost of that path
- We use priority queue to add paths, and update ans with max everytime
- pq is min heap since we want the shortest path

# Code
```cpp
class Solution {
public:

    class Cell {
    public:
        int t, x, y;
        Cell(int t, int x, int y) {
            this->t = t;
            this->x = x;
            this->y = y;
        }
        bool operator< (const Cell& other) const {
            return t > other.t;
        }
    };

    int swimInWater(vector<vector<int>>& grid) {
        int n = grid.size();
        int m = grid[0].size();
        static int dir[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};

        vector<vector<bool>> visited(n, vector<bool>(m, false));
        priority_queue<Cell> pq;

        pq.push(Cell(grid[0][0], 0, 0));

        int ans = 0;
        while(!pq.empty()) {
            auto rem = pq.top();
            pq.pop();

            ans = max(ans, rem.t);
            if(rem.x == n - 1 && rem.y == m - 1) return ans;

            for(auto d: dir) {
                int new_x = rem.x + d[0];
                int new_y = rem.y + d[1];

                if(new_x >= n || new_y >= m || new_x < 0 || new_y < 0 || visited[new_x][new_y]) continue;

                visited[new_x][new_y] = true;
                pq.push(Cell(grid[new_x][new_y], new_x, new_y));
            }
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/swim-in-rising-water/
