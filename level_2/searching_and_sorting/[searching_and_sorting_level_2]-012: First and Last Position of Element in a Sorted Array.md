# Problem Statement
1. Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.
2. If target is not found in the array, return [-1, -1].
3. You must write an algorithm with O(log n) runtime complexity.

[Tutorial](https://www.youtube.com/watch?v=Y7LiLNdayF0&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=13)

# Thought Process
- We will use two modified binary searches
- When finding starting index
  - Do a binary search. When element is found, store its index and continue binary search in left half
- When finding ending index
  - Do a binary search. When element is found, store its index and continue binary search in right half

# Code

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> ans = {-1, -1};
        int lo = 0, hi = size(nums) - 1;

        // Finding starting index
        while(lo <= hi) {
            int mid = (hi + lo) / 2;
            if(nums[mid] == target) {
                ans[0] = mid;
                hi = mid - 1;
            } else if(nums[mid] > target) {
                hi = mid - 1;
            } else {
                lo = mid + 1;
            }
        }

        lo = 0, hi = size(nums) - 1;
        // Finding ending index
        while(lo <= hi) {
            int mid = (hi + lo) / 2;
            if(nums[mid] == target) {
                ans[1] = mid;
                lo = mid + 1;
            } else if(nums[mid] > target) {
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
- https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/find-first-and-last-postion-of-element-in-sorted-array/ojquestion
