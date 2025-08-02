# Problem Statement
1. Given an array nums which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays.
2. Write an algorithm to minimize the largest sum among these m subarrays.

[Tutorial](https://www.youtube.com/watch?v=eq6dAJefOqc&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=24)

# Thought Process
- Same as Allocate Minimum Number of Books problem

# Code
```cpp
class Solution {
    bool isPossible(vector<int> nums, int mid, int m) {
        int splits = 1, sum = 0;

        for (int i = 0; i < (int)nums.size(); ++i) {
            sum += nums[i];

            if (sum > mid) {
                splits++;
                sum = nums[i];
            }
        }

        return splits <= m;
    }

public:
    int splitArray(vector<int>& nums, int m) {
        int ans = 0;
        int lo = *max_element(nums.begin(), nums.end());
        int hi = accumulate(nums.begin(), nums.end(), 0);

        while(lo <= hi) {
            int mid = lo + (hi - lo) / 2;

            if(isPossible(nums, mid, m)) {
                ans = mid;
                hi = mid - 1;
            } else {
                lo = mid + 1;
            }
        }

        return ans;
    }
};
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/split_array_largest_sum/ojquestion
- https://leetcode.com/problems/split-array-largest-sum/
