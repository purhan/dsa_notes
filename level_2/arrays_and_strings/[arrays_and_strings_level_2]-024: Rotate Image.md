# Problem Statement
You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

[Tutorial](https://www.youtube.com/watch?v=uB0RgD4p3LY&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=24)

# Thought Process
- Simple, find transpose of matrix and then reverse each row.
- Carefully examine the code for finding transpose (don't swap twice!, check for loop conditions), you have a habit of doing this wrong.

# Code
```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = size(matrix);
        for(int i = 0; i < n; ++i) {
            for(int j = 0; j < i; ++j) {
                swap(matrix[i][j], matrix[j][i]);
            }
        }

        for(int i = 0; i < n; ++i) {
            reverse(matrix[i].begin(), matrix[i].end());
        }
    }
};
```

# Problem Links
- https://leetcode.com/problems/rotate-image/
