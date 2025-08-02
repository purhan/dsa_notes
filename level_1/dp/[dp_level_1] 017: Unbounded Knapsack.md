# Problem Statement
1. You are given a number n, representing the count of items.
2. You are given n numbers, representing the values of n items.
3. You are given n numbers, representing the weights of n items.
3. You are given a number "cap", which is the capacity of a bag you've.
4. You are required to calculate and print the maximum value that can be created in the bag without 
    overflowing it's capacity.

Note -> Each item can be taken any number of times. You are allowed to put the same item again 
                  and again.

[Tutorial](https://www.youtube.com/watch?v=jgps7MXtKRQ&list=PL-Jc9J83PIiG8fE6rj9F5a6uyQ5WPdqKy&index=17)

# Thought Process

Recursive:
- Don't check for excluded case
- If an item is included, the remaining capacity again has n choices, so just run a for loop
- In other words:
- For each item, check for Unbounded Knapsack in the remaining capacity

Iterative:
- 1D DP contains max answer at each capacity
- If capacity is greater than or equal to current weight, we can try including this item. So we check max(include this item, or do nothing)
- If we include this item, we need to check answer at `cap-weight[i]`

# Code

Recursive:

```cpp
int helper(int& n, vector<int>& val, vector<int>& weight, int cap, vector<int>& dp) {
    if (cap <= 0) return 0;

    if (dp[cap] != -1) return dp[cap];

    int mx = 0;
    for (int i = 0; i < n; ++i) {

        if (weight[i] > cap) continue;

        int inc = val[i] + helper(n, val, weight, cap - weight[i], dp);
        mx = max(mx, inc);
    }

    return dp[cap] = mx;
}

void solve(int n, vector<int> val, vector<int> weight, int cap) {
    vector<int> dp(cap + 1, -1);
    cout << helper(n, val, weight, cap, dp);
}
```

Iterative:

```cpp
void solve(int n, vector<int> val, vector<int> weight, int cap) {
    vector<int> dp(cap + 1, 0);

    for (int c = 1; c <= cap; ++c) {
        for (int i = 0; i < n; ++i) {
            if (weight[i] <= c) {
                int inc = val[i] + dp[c - weight[i]];
                dp[c] = max(dp[c], inc);
            }
        }
    }

    cout << dp[cap] << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/dynamic-programming-and-greedy/unbounded-knapsack-official/ojquestion#!
