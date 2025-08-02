# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/139428264-8d6fce4f-5780-47d4-82c3-4a3034d9ecda.png)

[Tutorial](https://www.youtube.com/watch?v=MwDM7XYjidc&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=57)

# Thought Process

> You REALLY DONT KNOW HOW TO TRAVERSE ON ALL DIAGONALS

- For all diagonals, use swap sort
- For traversing on all diagonals,

![image](https://user-images.githubusercontent.com/10897423/139428420-fbc6bddd-b39d-44a0-9ef0-6128da11bd5a.png)

- All diagonals either start from a leftmost or a topmost element
- For all leftmost elements (all elements in first col) and all topmost elements (all elements in first row), use two pointers r and c and increment both equally untill youre out of the matrix

# Code
```cpp
class Solution {
    void countSort(int n, int m, vector<vector<int>>& mat, int row, int col) {
        map<int, int> cnt;

        // Traverse on diagonal starting from that row/col
        int r = row, c = col;
        while(r < n && c < m) {
            cnt[mat[r][c]]++;
            r++;
            c++;
        }

        // Traverse on diagonal again
        r = row, c = col;
        int cur = cnt[0];
        for(auto [k, v]: cnt) {
            while(v--) {
                mat[r][c] = k;
                r++;
                c++;
            }
        }
    }
public:
    vector<vector<int>> diagonalSort(vector<vector<int>>& mat) {
        int n = size(mat), m = size(mat[0]);

        // Traverse on first col
        for(int i = 0; i < n; ++i) {
            countSort(n, m, mat, i, 0);
        }

        // Traverse on each row
        for(int i = 1; i < m; ++i) {
            countSort(n, m, mat, 0, i);
        }

        return mat;
    }
};
```

# Problem Links
- https://leetcode.com/problems/sort-the-matrix-diagonally/
