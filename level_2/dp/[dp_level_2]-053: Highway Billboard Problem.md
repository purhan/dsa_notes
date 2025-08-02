# Problem Statement

1. You are given a number M representing length of highway(range).

2. You are given a number N representing number of bill boards.

3. You are given N space separated numbers representing (P)position of bill-boards.

4. You are given N space separated numbers representing (R)revenue corresponding to each (P)position.

5. You are given a number T such that bill-boards can only be placed after specific distance(T).

6. Find the maximum revenue that can be generated.

[Tutorial](https://www.youtube.com/watch?v=SiGqwJOvflE&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=54)

# Thought Process
- Based on LIS only
- I first wrote O(n^2) approach, same as LIS, but that gave TLE
- There is an O(m) approach, read code to understand it

# Code

solution not working but good for understanding:

```cpp
void solve(int n, int m, vector<int> pos, vector<int> rate, int t) {
    vector<int> dp(m + 1);

    // construct a map to check if a board exists at xth mile
    map<int, int> board;
    for (int i = 0; i < n; ++i) board[pos[i]] = rate[i];

    for (int i = 1; i <= m; ++i) {

        // If we don't choose this board
        dp[i] = dp[i - 1];

        // if board exists here, we have choice between choosing it or not choosing
        if (board[i] > 0) {
            dp[i] = max(dp[i], board[i] + dp[i - t - 1]);
        }
    }

    cout << dp[m] << endl;
}
```

working code:

```cpp
void solve(int n, int m, vector<int> pos, vector<int> rate, int t) {
    vector<int> dp(m + 1);

    // construct a map to check if a board exists at xth mile
    map<int, int> board;
    for (int i = 0; i < n; ++i) board[pos[i]] = rate[i];

    for (int i = 1; i <= m; ++i) {
        dp[i] = dp[i - 1];
        if (board[i] > 0) {
            if (i >= t + 1) {
                dp[i] = max(dp[i], board[i] + dp[i - t - 1]);
            } else {
                dp[i] = max(dp[i], board[i]);
            }
        }
    }

    cout << dp[m] << endl;
}
```

# Problem Links
