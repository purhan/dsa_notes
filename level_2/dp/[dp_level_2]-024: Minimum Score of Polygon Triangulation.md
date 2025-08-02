# Problem Statement
1. You are given an array of integers, which represents the vertices of an N-sided convex polygon in clockwise order.
2. You have to triangulate the given polygon into N-2 triangles.
3. The value of a triangle is the product of the labels of vertices of that triangle.
4. The total score of the triangulation is the sum of the value of all the triangles.
5. You have to find the minimum score of the triangulation of the given polygon.

[Tutorial](https://www.youtube.com/watch?v=tmIhmeL8WRo&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=27)

# Thought Process
- This uses Catalan Numbers

# Code
```cpp
class Solution {
public:
    int minScoreTriangulation(vector<int>& nums) {
        int n = size(nums);
        vector<vector<int>> dp(n - 1, vector<int>(n - 1, 0));

        for(int g = 0; g < n - 1; ++g) {
            for(int i = 0, j = g; j < n - 1; ++i, ++j) {
                if(g == 0) {
                    dp[i][j] = 0;
                } else if(g == 1) {
                    dp[i][j] = nums[i] * nums[j] * nums[j + 1];
                } else {
                    int mn = INT_MAX;
                    for(int k = i; k < j; ++k) {
                        int lc = dp[i][k];
                        int rc = dp[k + 1][j];
                        int mc = nums[i] * nums[k + 1] * nums[j + 1];
                        mn = min(mn, lc + rc + mc);
                    }

                    dp[i][j] = mn;
                }
            }
        }

        return dp[0][n - 2];
    }
};
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/minimum-score-of-triangulation-official/ojquestion
- https://leetcode.com/problems/minimum-score-triangulation-of-polygon/