# Problem Statement

1. You are given a number n, representing the number of bridges on a river.
2. You are given n pair of numbers, representing the north bank and south bank co-ordinates of each bridge.
3. You are required to print the count of maximum number of non-overlapping bridges.

[Tutorial](https://www.youtube.com/watch?v=o1h3aoeSTOU&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=4)

# Thought Process

- Create a 1-D DP
- Sort based on north bank
- Find LIS for south bank

# Code

```cpp
int solve(vector<pair<int, int>> bridges, int n) {
    sort(bridges.begin(), bridges.end());
    vector<int> dp(n + 1, 0);
    dp[0] = 1;

    for (int i = 1; i < n; ++i) {
        for (int j = 0; j < i; ++j) {
            if (bridges[i].second > bridges[j].second)
                dp[i] = max(dp[i], dp[j]);
        }
        dp[i]++;
    }

    return *max_element(dp.begin(), dp.end());
}
```

# Problem Links
https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/max-non-overlapping-bridges-official/ojquestion#!
https://leetcode.com/problems/best-team-with-no-conflicts/