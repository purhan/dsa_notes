# Problem Statement
1. You are given an array of integers(arr).
2. You have to find the count of equivalent subarrays.
3. A subarray is equivalent if, count of unique integers in the subarray = count of unique integers in the given array.

[Tutorial](https://www.youtube.com/watch?v=ceRJzjBrhPU&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=19)

# Thought Process
- Uses acquire release strategy
- We start with two pointers, start acquiring numbers till we have acquired `k` unique numbers (determined by map size)
- Once we acquire k unique nums, we add `n - r` to the answer. WHY? Look at the screenshot below

![image](https://user-images.githubusercontent.com/10897423/136826390-6dae8e2d-8ed4-44ca-90a0-9663c81abea7.png)

- For this subarray, there are `n - r - 1` more subarrays till the last element of the array that satisfy the same condition

- Then, we start releasing from left and keep adding `n - r` to the answer until we reach an invalid subarray

# Code
```cpp
void solve(vector<int> nums, int n) {
    // first take count of distinct elements
    map<int, int> hashmap;
    for (auto i : nums) freq[i]++;
    int k = freq.size();

    // create two pointers
    freq.clear();
    int l = -1, r = -1;
    int ans = 0;

    while (r < n) {
        r++;
        int acq = nums[r];  // number just acquired
        freq[acq]++;

        if (freq.size() == k) {
            ans += n - r;
            while (l <= r) {
                l++;
                int rel = nums[l];  // number just released
                freq[rel]--;

                if (freq[rel] == 0) freq.erase(rel);

                if (freq.size() == k) {
                    ans += n - r;
                } else {
                    break;
                }
            }
        }
    }
    cout << ans;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/equivalent-subarrays-official/ojquestion#!
