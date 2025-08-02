# Problem Statement
1. You are given a number n, representing the number of elements.
2. You are required to find the number of Binary Search Trees you can create using the elements.

[Tutorial](https://www.youtube.com/watch?v=H1qjjkm3P3c&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=16)

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/134689504-49885023-f549-4e24-9b55-61354479b246.png)

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
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/count-bst-official/ojquestion
- https://leetcode.com/problems/unique-binary-search-trees/
