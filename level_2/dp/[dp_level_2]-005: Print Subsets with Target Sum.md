# Problem Statement
1. You are given a number n, representing the count of elements.
2. You are given n numbers.
3. You are given a number "tar".
4. You are required to calculate and print true or false, if there is a subset the elements of which add up to "tar" or not.
5. Also, you have to print the indices of elements that should be selected to achieve the given target.
6. You have to print all such configurations.

[Tutorial](https://www.youtube.com/watch?v=qtqMTgmDpQg&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=5)

# Thought Process


# Code
```cpp
class Pair {
public:
    int i, j;
    string psf;

    Pair(int i1, int j1, string psf1) {
        this->i = i1;
        this->j = j1;
        this->psf = psf1;
    }
};

void solve(vector<int> nums, int n, int target) {
    vector<vector<int>> dp(n + 1, vector<int>(target + 1, 0));

    dp[0][0] = 1;
    for (int i = 1; i <= n; ++i) {
        for (int j = 0; j <= target; ++j) {
            if (j == 0) {
                dp[i][j] = 1;
            } else {
                // In case this item gets included in subset
                dp[i][j] = dp[i][j] || dp[i - 1][j];

                // In case this item gets excluded in subset
                if (j >= nums[i - 1])
                    dp[i][j] = dp[i][j] || dp[i - 1][j - nums[i - 1]];
            }
        }
    }

    cout << (dp[n][target] ? "true\n" : "false\n");

    queue<Pair> q;
    q.push(Pair(n, target, ""));

    while (!q.empty()) {
        auto f = q.front();
        q.pop();

        if (f.i == 0 || f.j == 0) {
            cout << f.psf << endl;
        } else {

            // In case this item gets included in subset
            if (f.j >= nums[f.i - 1]) {
                bool inc = dp[f.i - 1][f.j - nums[f.i - 1]];
                if (inc) {
                    q.push(Pair(f.i - 1, f.j - nums[f.i - 1], to_string(f.i - 1) + " " + f.psf));
                }
            }

            // In case this item gets included in subset
            bool exc = dp[f.i - 1][f.j];
            if (exc) {
                q.push(Pair(f.i - 1, f.j, f.psf));
            }
        }

    }
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/print-all-paths-with-target-sum-subset-official/ojquestion
