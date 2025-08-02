# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/144864800-232d9d84-fa51-4503-be0f-b341b85a4b55.png)

[Tutorial](https://www.youtube.com/watch?v=TTdEaEQCPik&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=67)

# Thought Process
- Think of the arrangement like this:

![image](https://user-images.githubusercontent.com/10897423/144864728-5ca7d28b-7705-4084-9c84-59c8bc32ecb2.png)

- Pretty straightforward simulation after that

# Code
```cpp
class Solution {
public:
    double champagneTower(int poured, int query_row, int query_glass) {
        vector<vector<double>> g(query_row + 2, vector<double>(query_row + 2));

        g[0][0] = poured;
        for(int i = 0; i <= query_row; ++i) {
            for(int c = 0; c <= i; ++c) {
                if(g[i][c] > 1) {
                    double val = g[i][c] - 1;
                    g[i][c] = 1;
                    g[i + 1][c] += val / 2;
                    g[i + 1][c + 1] += val / 2;
                }
            }
        }
        return g[query_row][query_glass];
    }
};
```

# Problem Links
- https://leetcode.com/problems/champagne-tower/
