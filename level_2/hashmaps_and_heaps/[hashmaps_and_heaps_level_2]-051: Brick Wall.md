# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/137483513-4dcea49c-b498-48fa-bb13-ab8bf05e26d0.png)

[Tutorial](https://www.youtube.com/watch?v=bKt63YABdNw&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=51)

# Thought Process
- For each cross-section of the wall, we have to find the minimum walls you will be intersecting at any point
- Say the wall has `n` rows
- For all rows, we will store the empty index (index at which no wall is present, which is any index where a wall is ending)
  - We will store this index in a map.

- Then, we will traverse through the map and check at which index, most number of walls are ending, so we will encounter least number of walls at that index

# Code
```cpp
class Solution {
public:
    int leastBricks(vector<vector<int>>& wall) {
        map<int, int> freq; // freq of wall ending at width map[key]

        // find out number of walls ending at each width
        for(auto row: wall) {
            int currWidth = 0;
            for(int i = 0; i < row.size() - 1; ++i) {
                currWidth += row[i];
                freq[currWidth]++;
            }
        }

        // for each integer width, if `x` walls end here, then you will intersect `n - x` walls
        int ans = wall.size();
        for(auto [width, f]: freq) {
            ans = min(ans, (int)wall.size() - f);
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/brick-wall/
