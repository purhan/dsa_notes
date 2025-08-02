# Problem Statement
1. You are given a number n, representing the count of items.
2. You are given n numbers, representing the values of n items.
3. You are given n numbers, representing the weights of n items.
3. You are given a number "cap", which is the capacity of a bag you've.
4. You are required to calculate and print the maximum value that can be created in the bag without 
     overflowing it's capacity.

Note -> Each item can be taken 0 or 1 number of times. You are not allowed to put the same item 
               again and again.

[Tutorial](https://www.youtube.com/watch?v=bUSaenttI24&list=PL-Jc9J83PIiG8fE6rj9F5a6uyQ5WPdqKy&index=16)

# Thought Process

Recursive:
- Each item can either be included or excluded, check both scenarios recursively
- If weight of an item is greater than capacity, only check for exclusion scenario
- Else check for both scenarios and return the greater one
- Base condition: iterator goes outside array, or capacity becomes zero or negative (then no need to check further, all items will be excluded after that)

Iterative:
- Table cell represents [item vs capacity]
- For each item, if we include that item, its value will be `val[i] + dp[i - 1][j - weight[i]]`
- If we exclude that item, its value will be `dp[i - 1][unchanged i.e. j]`

# Code

Recursive:

```cpp
int helper(int n, vector<int>& val, vector<int>& weight, int cap, int i, vector<vector<int>>& dp) {
    if (dp[i][cap] != -1) return dp[i][cap];
    if (i >= (int)val.size() || cap <= 0) {
        return 0;
    }

    int inc = val[i] + helper(n, val, weight, cap - weight[i], i + 1, dp);
    int exc = helper(n, val, weight, cap, i + 1, dp);

    if (weight[i] > cap) return dp[i][cap] = exc;
    else return dp[i][cap] = max(inc, exc);
}

void solve(int n, vector<int> val, vector<int> weight, int cap) {
    vector<vector<int>> dp(weight.size() + 1, vector<int>(cap + 1, -1));
    cout << helper(n, val, weight, cap, 0, dp);
}
```

Iterative:

```cpp
void solve(int n, vector<int> val, vector<int> weight, int cap) {
    vector<vector<int>> dp(weight.size() + 1, vector<int>(cap + 1, 0));

    for (int j = 0; j <= cap; ++j) {
        if (j >= weight[0]) dp[0][j] = val[0];
    }

    for (int i = 1; i <= n; ++i) {
        for (int j = 0; j <= cap; ++j) {

            int inc = (j >= weight[i])                      // to avoid segmentation fault
                      ? val[i] + dp[i - 1][j - weight[i]]
                      : 0;

            int exc = dp[i - 1][j];

            dp[i][j] = max(inc, exc);
        }
    }
    cout << dp[n][cap] << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/dynamic-programming-and-greedy/zero-one-knapsack-official/ojquestion#!
