# Problem Statement
1. You are given an array that contains only 0s, 1s, and 2s.
2. You have to find length of the longest subarray with equal number of 0s, 1s, and 2s.

[Tutorial](https://www.youtube.com/watch?v=MRoWBJvJeLQ&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=33)

# Thought Process
- Keep track of `cnt1 - cnt0 v/s cnt2 - cnt1`, if this value ever repeats, we have a subarray that satisfies the condition. Take max of all such subarrays

# Code
```cpp
void solve(vector<int> nums, int n) {
    int ans = 0;
    vector<int> cnt(3, 0);
    map<pair<int, int>, int> firstOccurenceOfDiff;

    firstOccurenceOfDiff[ {0, 0}] = -1;
    for (int i = 0; i < n; ++i) {
        int x = nums[i];
        cnt[x]++;
        pair<int, int> currDiff = {cnt[1] - cnt[0], cnt[2] - cnt[1]};

        if (firstOccurenceOfDiff[currDiff]) {
            ans = max(ans, i - firstOccurenceOfDiff[currDiff]);
        } else {
            firstOccurenceOfDiff[currDiff] = i;
        }
    }

    cout << ans;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/longest-subarray-with-equal-number-of-0s-1s-and-2s-official/ojquestion