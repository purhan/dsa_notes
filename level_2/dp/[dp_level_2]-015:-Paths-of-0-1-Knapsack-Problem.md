# Problem Statement
1. You are given a number n, representing the count of items.
2. You are given n numbers, representing the values of n items.
3. You are given n numbers, representing the weights of n items.
3. You are given a number "cap", which is the capacity of a bag you've.
4. You are required to calculate and print the maximum value that can be created in the bag without overflowing it's capacity.
5. Also, you have to print the indices of items that should be selected to make maximum profit.
6. You have to print all such configurations.

Note - Each item can be taken 0 or 1 number of times. You are not allowed to put the same item again and again.

[Tutorial](https://www.youtube.com/watch?v=YH6M9WFp02g&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=15)

# Thought Process

# Code
```cpp
class Pair {
public:
    int i;
    int j;
    string psf;

    Pair(int i1, int j1, string psf1) {
        this->i = i1;
        this->j = j1;
        this->psf = psf1;
    }
};

void solve(vector<int> val, vector<int> wt, int cap, int n) {
    vector<vector<int>> dp(n + 1, vector<int>(cap + 1, 0));

    for (int i = 1; i <= n; ++i) {
        for (int j = 1; j <= cap; ++j) {
            dp[i][j] = dp[i - 1][j];

            if (j >= wt[i - 1]) {
                dp[i][j] = max(dp[i][j], dp[i - 1][j - wt[i - 1]] + val[i - 1]);
            }
        }
    }
    cout << dp[n][cap] << endl;

    queue<Pair> q;
    q.push(Pair(n, cap, ""));

    while (!q.empty()) {
        Pair rem(q.front());
        q.pop();

        if (rem.i == 0 || rem.j == 0) {
            cout << rem.psf << endl;
        } else {
            int exc = dp[rem.i - 1][rem.j];

            if (rem.j >= wt[rem.i - 1]) {
                int inc = dp[rem.i - 1][rem.j - wt[rem.i - 1]] + val[rem.i - 1];
                if (dp[rem.i][rem.j] == inc) {
                    q.push(Pair(rem.i - 1, rem.j - wt[rem.i - 1], to_string(rem.i - 1) + " " + rem.psf));
                }
            }

            if (dp[rem.i][rem.j] == exc) {
                q.push(Pair(rem.i - 1, rem.j, rem.psf));
            }
        }
    }
}
```

# Problem Links
https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/zero-one-knapsack-re-official/ojquestion