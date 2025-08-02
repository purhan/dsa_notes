# Problem Statement
1. You are given an array(arr) of positive integers of length N which represents the dimensions of N-1 matrices such that the ith matrix is of dimension arr[i-1] x arr[i].
2. You have to find the minimum number of multiplications needed to multiply the given chain of matrices.

[Tutorial](https://www.youtube.com/watch?v=pEYwLmGJcvs&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=24)

# Thought Process
To avoid confusion with catalan numbers in the future, here's a quote from Stackoverflow:

> Matrix Chain Multiplication and Parenthesization Problem [Catalan Numbers] are equilvaent form of one another. One can be reduced into another.

- Create a 2D DP if size `nums.size() - 1`
- This uses gap strategy

![image](https://user-images.githubusercontent.com/10897423/134765519-4445eeeb-66a6-4112-a5a4-1b979dbc47cf.png)

- Watch tutorial at 7:30 for better insight on the above screenshot

![image](https://user-images.githubusercontent.com/10897423/134765675-cf292d8f-0da1-4de5-8cbd-9c6c95689709.png)

- Check the above screenshot and check the code for better idea. Check which cells are highlighted in which color

# Code
```cpp
void solve(int n, vector<int> nums) {
    vector<vector<int>> dp(n - 1, vector<int>(n - 1, 0));

    for (int g = 0; g < n - 1; ++g) {
        for (int i = 0, j = g; j < n - 1; ++i, ++j) {
            if (g == 0) {
                // No multiplication possible in 1 matrix
                dp[i][j] = 0;
            } else if (g == 1) {
                // Straightforward in 2 matrices
                dp[i][j] = nums[i] * (nums[j] * nums[j + 1]);
            } else {
                int mn = INT_MAX;
                for (int k = i; k < j; ++k) {
                    int left_cost = dp[i][k];
                    int right_cost = dp[k + 1][j];
                    int multiplication_cost = nums[i] * nums[k + 1] * nums[j + 1];

                    mn = min(mn, left_cost + right_cost + multiplication_cost);
                }
                dp[i][j] = mn;
            }
        }
    }

    cout << dp[0][n - 2] << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/matrix-chain-multiplication-official/ojquestion
