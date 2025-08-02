# Problem Statement

1. You are given a number n, representing the number of elements.
2. You are given n numbers, representing the contents of array of length n.
3. You are required to print the length of longest bitonic subsequence of array.
Note - Bitonic subsequences begin with elements in increasing order, followed by elements in decreasing order.

[Tutorial](https://www.youtube.com/watch?v=jdfpGSSyN2I&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=3)

# Thought Process

- Create two 1-D DPs
- One stores LIS, other stores LDS
- Calculate LIS **ending at that cell** for each cell
- Calculate LDS **starting at that cell** for each cell
- Answer is maximum value of `lis[i] + lds[i]` for each cell

# Code

```cpp
int solve(vector<int> nums, int n) {
    vector<int> lis(n + 1, 0);
    vector<int> lds(n + 1, 0);
    lis[0] = 1;
    lis[0] = 1;
    int ans = 0;

    for (int i = 1; i < n; ++i) {
        for (int j = 0; j < i; ++j) {
            if (nums[i] > nums[j]) {
                lis[i] = max(lis[i], lis[j]);
            }
        }
        lis[i]++;
    }

    for (int i = n - 1; i >= 0; --i) {
        for (int j = n - 1; j > i; --j) {
            if (nums[i] >= nums[j]) {
                lds[i] = max(lds[i], lds[j]);
            }
        }
        lds[i]++;
        ans = max(ans, lis[i] + lds[i] - 1);
    }

    return ans;
}

```

# Problem Links
https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/lbs-official/ojquestion
https://leetcode.com/problems/minimum-number-of-removals-to-make-mountain-array/