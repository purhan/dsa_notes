# Problem Statement
1. You are given a number N, which represents the number of sides in a polygon.
2. You have to find the total number of ways in which the given polygon can be triangulated.

[Tutorial](https://www.youtube.com/watch?v=jSGW3YKkyHQ&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=20)

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/134704735-1754b923-b8d3-494d-9d6a-bb1cf5f4a43f.png)

- Solution is just Catalan Numbers, think about how to show that to the interviewer
- Screenshot may be useful, we traverse from 1 ... n, and come up with the equation (recurrence relation) somewhere around n = 3 or 4


# Code
```cpp
void solve(int n) {

    n -= 2; // A polygon has atleast 3 sides

    vector<int> dp(n + 1, 0);
    dp[0] = 1;
    dp[1] = 1;

    for (int i = 2; i <= n; ++i) {
        for (int j = 0; j < i; ++j) {
            dp[i] += dp[j] * dp[i - j - 1];
        }
    }

    cout << dp[n];
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/number-of-ways-of-triangulation-official/ojquestion#!
