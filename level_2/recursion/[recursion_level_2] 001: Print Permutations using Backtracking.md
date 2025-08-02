# Problem Statement

Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

[Tutorial](https://www.youtube.com/watch?v=QKkHCS5bq0I&list=PL-Jc9J83PIiHO9SQ6lxGuDsZNt2mkHEn0)

# Thought Process

> LC Question slightly different from tutorial

# Code
```cpp
class Solution {
    void helper(vector<int>& nums, int currItem, vector<vector<int>>& ans) {
        if(currItem >= nums.size()) {
            ans.push_back(nums);
            return;
        }
        for(int i = currItem; i < nums.size(); ++i) {
            swap(nums[currItem], nums[i]);
            helper(nums, currItem + 1, ans);
            swap(nums[i], nums[currItem]);
        }
    }
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> ans;

        helper(nums, 0, ans);
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/permutations/
