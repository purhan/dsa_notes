# Problem Statement

**Prerequisite: Longest Increasing Subsequence**
1. You are given a number n, representing the number of elements.
2. You are given n numbers, representing the contents of array of length n.
3. You are required to print the sum of elements of the increasing subsequence with maximum sum for the array.

[Tutorial](https://www.youtube.com/watch?v=5ToHur2XrA4&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=3)

# Thought Process

- Create a 1-D DP

![image](https://user-images.githubusercontent.com/10897423/133922265-89c2f732-3ffe-435c-af33-b33816dbad09.png)

- Each cell stores the **maximum sum LIS that ends at that element**
- We check all previous cells that have `num[j] < num[i]` (Because only then the sequence would be `increasing`)

# Code

```cpp
int solve(vector<int> nums, int n) {
    vector<int> dp(n + 1, 0);
    dp[0] = nums[0];

    for (int i = 1; i < n; ++i) {
        for (int j = 0; j < i; ++j) {
            if (nums[i] >= nums[j]) {
                dp[i] = max(dp[i], dp[j]);
            }
        }
        dp[i] += nums[i];
    }

    return *max_element(dp.begin(), dp.end());
}
```

# Problems:
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/msis-official/ojquestion
- https://leetcode.com/problems/best-team-with-no-conflicts/