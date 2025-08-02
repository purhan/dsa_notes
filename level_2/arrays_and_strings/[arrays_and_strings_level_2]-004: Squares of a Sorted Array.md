# Problem Statement
Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

[Tutorial](https://www.youtube.com/watch?v=u3A64HQq_Dw&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=4)

# Thought Process

# Code
```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        int n = size(nums);
        vector<int> ans(n, 0);

        int i = 0, j = n - 1;
        for(int k = n - 1; k >= 0; --k) {
            if(nums[i] < 0) {
                if(abs(nums[i]) > nums[j]) {
                    ans[k] = nums[i] * nums[i];
                    i++;
                } else {
                    ans[k] = nums[j] * nums[j];
                    j--;
                }
            } else {
                ans[k] = nums[j] * nums[j];
                j--;
            }
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/squares-of-a-sorted-array/
