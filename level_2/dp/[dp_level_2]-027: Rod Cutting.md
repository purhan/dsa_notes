# Problem Statement
1. You are given an integer N, which represents the length of a rod, and an array of integers, which represents the prices of rod pieces of length varying from 1 to N.
2. You have to find the maximum value that can be obtained by selling the rod.
3. You can sell it in pieces or as a whole.

[Tutorial](https://www.youtube.com/watch?v=eQuJb5gBkkc&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=28)

# Thought Process
- Tutorial was unnecessarily long. But it shows 2 different methods to solve this. Here I'm only writing one
- We need a 1D DP to store the maximum price of a rod of length `x`
- While traversing, we will check the maximum price of length `y`, and to that we can add the price of length `x - y` to get the max price of `x`
- This is kinda similar to coin change imo

![image](https://user-images.githubusercontent.com/10897423/134915676-d20679d0-2d7f-42b8-a4f0-df52c9e7f7c6.png)

- Screenshot shows:
  - Absolute price (If we don't cut the rod) of length `x` at the top. This array is given to us
  - Maximum price (or optimized price) of any rod of length `x`
  - For example, if we want the max price of `3`, we can find the max of:
    - Price of `0` + price of `3`
    - Price of `1` + price of `2`
    - ~~Price of `2` + price of `1`~~ (repeated, unnecessary)

# Code
```cpp
void solve(vector<int> nums, int n) {
    vector<int> dp(n + 1, 0);

    for (int i = 1; i <= n; ++i) {
        for (int j = 0; j <= i; ++j) {
            dp[i] = max(dp[i], dp[j] + nums[i - j - 1]);
        }
    }

    cout << *max_element(dp.begin(), dp.end());
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/rod-cutting-official/ojquestion
