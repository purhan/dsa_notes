# Problem Statement
1. You are given a number N.
2. There are 2*N points on a circle. You have to draw N non-intersecting chords on a circle.
3. You have to find the number of ways in which these chords can be drawn.

[Tutorial](https://www.youtube.com/watch?v=qgQg1BcCWBA&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=19)

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/134699747-5d1bc40b-6680-40fa-aba4-7b5a4fc6f50b.png)

- Solution is just Catalan Numbers, think about how to show that to the interviewer
- Screenshot may be useful, we traverse from 1 ... n, and come up with the equation (recurrence relation) somewhere around n = 3 or 4


# Code
```cpp
void solve(int n) {
    n /= 2;
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
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/circle-and-chords-official/ojquestion
