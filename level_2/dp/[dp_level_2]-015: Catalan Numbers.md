# Problem Statement
1. You are given a number n.
2. You are required to find the value of nth catalan number.

C0 - 1

C1 - 1

C2 - 2

C3 - 5

.....

Cn = C0.Cn-1 + C1.Cn-2 + .. + Cn-2.C1 + Cn-1.C0

[Tutorial](https://www.youtube.com/watch?v=eUw9A1wsFg8&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=15)

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/134680523-35e7b85b-f61b-4abc-a08f-07bc0460e26e.png)

- We just have to store in dp[i] this value: `C0.Cn-1 + C1.Cn-2 + .. + Cn-2.C1 + Cn-1.C0`


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
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/catalan-number-official/ojquestion
