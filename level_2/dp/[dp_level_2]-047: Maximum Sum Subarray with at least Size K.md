# Problem Statement
1. You are given an array(arr) of integers and a number k.
2. You have to find maximum subarray sum in the given array.
3. The subarray must have at least k elements.

[Tutorial](https://www.youtube.com/watch?v=OodoQ95se20&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=48)

# Thought Process

# Code
```cpp
void solve(vector<int> nums, int k, int n) {
    int ans = INT_MIN;

    vector<int> pre(n);

    int csum = nums[0];
    pre[0] = csum;
    for (int i = 1; i < n; ++i) {
        if (csum > 0) {
            csum += nums[i];
        } else {
            csum = nums[i];
        }

        pre[i] = csum;
    }

    int exactK = 0;
    for (int i = 0; i < k; ++i) {
        exactK += nums[i];
    }

    ans = max(ans, exactK);

    for (int i = k; i < n; ++i) {
        exactK += nums[i] - nums[i - k];

        ans = max(ans, exactK);

        int moreThanK = pre[i - k] + exactK;

        ans = max(ans, moreThanK);
    }

    cout << ans;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/maximum-sum-subarray-with-at-least-k-elements-official/ojquestion
