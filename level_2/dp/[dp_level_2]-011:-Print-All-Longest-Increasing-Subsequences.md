# Problem Statement
1. You are given a number N representing number of elements.
2. You are given N space separated numbers (ELE : elements).
3. Your task is to find & print  
    3.1) Length of "Longest Increasing Subsequence"(LIS).
    3.2) All "Longest Increasing Subsequence(s)"(LIS).

[Tutorial](https://www.youtube.com/watch?v=3mD20VSib5E&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=11)

# Thought Process
- Create a 1D DP
- First calculate Longest Increasing Subsequences normally
- Now, put the highest value from DP into a queue. Basically we want to do a BFS from `mx -> mx-1 -> mx-2 -> ..... 1` where `mx` is the length of LIS

# Code
```cpp
class Path {
public:
    int l;
    int i;
    int val;
    string psf;

    Path(int l, int i, int val, string psf) {
        this->l = l;
        this->i = i;
        this->val = val;
        this->psf = psf;
    }
};

void solve(vector<int> nums, int n) {
    vector<int> dp(n, 0);
    dp[0] = 1;
    int mx = 1;

    for (int i = 1; i < n; ++i) {
        for (int j = 0; j < i; ++j) {
            if (nums[i] > nums[j]) {
                dp[i] = max(dp[i], dp[j]);
            }
        }
        dp[i]++;
        mx = max(mx, dp[i]);
    }
    cout << mx << endl;

    ///// Till here, same as LIS /////

    queue<Path*> q;
    for (int i = 0; i < n; ++i) {
        if (mx == dp[i]) {
            Path* x = new Path(mx, i, nums[i], to_string(nums[i]));
            q.push(x);
        }
    }

    while (!q.empty()) {
        auto f = q.front();
        q.pop();

        if (f->l == 1) {
            cout << f->psf << endl;
        }

        for (int j = f->i; j >= 0; --j) {
            if (dp[j] == f->l - 1 && nums[j] <= f->val) {
                q.push(new Path(dp[j], j, nums[j], to_string(nums[j]) + " -> " + f->psf));
            }
        }
    }
}
```

# Problem Links
https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/lis-re-official/ojquestion