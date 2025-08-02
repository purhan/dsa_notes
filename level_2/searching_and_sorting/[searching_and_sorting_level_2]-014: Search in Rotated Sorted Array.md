# Problem Statement
1. There is an integer array nums sorted in ascending order (with distinct values).
2. nums is rotated at an unknown pivot index k (0 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].
3. Given the array nums after the rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.
4. You must write an algorithm with O(log n) runtime complexity.

[Tutorial](https://www.youtube.com/watch?v=1uu3g_uu8O0&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=14)

# Thought Process
- Do a binary search
- If element at `lo` is less than `mid`
  - If `target` is between `lo` and `mid`, left half is sorted. Look up the left half
  - Else left half is unsorted. Look up the right half
- If element at `mid` is less than `hi`
  - If `target` is between `mid` and `hi`, right half is sorted. Look up the right half
  - Else right half is unsorted, look up the left half

# Code
```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int n = size(nums);
        int lo = 0, hi = n - 1;

        while (lo <= hi) {
            int mid = (lo + hi) / 2;

            if (nums[mid] == target) {
                return mid;
            } else if (nums[lo] <= nums[mid]) {
                // left half is sorted
                if (target >= nums[lo] && target < nums[mid]) {
                    hi = mid - 1;
                } else {
                    lo = mid + 1;
                }
            } else if (nums[mid] <= nums[hi]) {
                // right half is sorted
                if (target > nums[mid] && target <= nums[hi]) {
                    lo = mid + 1;
                } else {
                    hi = mid - 1;
                }
            }
        }

        return -1;
    }
};
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/search_in_rotated_sorted_array/ojquestion
- https://leetcode.com/problems/search-in-rotated-sorted-array/
