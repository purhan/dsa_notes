# Problem Statement
1. You are given a number n, representing the number of upstrokes / and number of downstrokes .
2. You are required to find the number of valleys and mountains you can create using strokes.

Note - At no point should we go below the sea-level. (number of downstrokes should never be more than number of upstrokes).

[Tutorial](https://www.youtube.com/watch?v=hM_FJnrP1kk&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=17)

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/134691845-c63aa413-8269-4980-9e6e-66e48fdfa019.png)

- Solution is just Catalan Numbers, think about how to show that to the interviewer
- Screenshot may be useful, we traverse from 1 ... n, and come up with the equation (recurrence relation) somewhere around n = 3 or 4


# Code
```cpp
void solve(int n) {
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
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/count-valleys-mountains-official/ojquestion
