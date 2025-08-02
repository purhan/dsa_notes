# Problem Statement
1. You are given a number n.
2. You are required to print the number of binary strings of length n with no consecutive 0's.

[Tutorial]()

# Thought Process

Recursive:

Iterative:

# Code

Recursive:

```cpp
```

Iterative:

```cpp
void solve(int n) {
    vector<int> dp(n + 1);      // dp[x] = number of binary strings of size x

    dp[0] = 1;  // no string of size 0, only one possible combination
    dp[1] = 2;  // string either `1` or `0`
    for (int i = 2; i <= n; ++i) {
        dp[i] = dp[i - 1]       // if zero at this index
                + dp[i - 2];    // if one at this index, then can't choose previous index
    }

    cout << dp[n];
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/dynamic-programming-and-greedy/count-binary-strings-official/ojquestion
