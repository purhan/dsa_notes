# Problem Statement

Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times.

[Tutorial](https://www.youtube.com/watch?v=1QybAZMCYhA&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=6)

> Next problem, majority element general, will NOT use boyer-moore algo and can NOT be dont in O(n). It will use simple freq map so I'm not creating notes for it

# Thought Process
- At most, 2 elements can have freq >= n/3
- Create 2 candidates and use boyer-moore algo

# Code
```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        int n = size(nums);
        int val1 = 0, cnt1 = 0, val2 = 0, cnt2 = 0;

        for(int i = 0; i < n; ++i) {
            if(nums[i] == val1) {
                cnt1++;
            } else if(nums[i] == val2) {
                cnt2++;
            } else {
                if(cnt1 == 0) {
                    cnt1 = 1;
                    val1 = nums[i];
                } else if(cnt2 == 0) {
                    cnt2 = 1;
                    val2 = nums[i];
                } else {
                    cnt1--;
                    cnt2--;
                }
            }
        }

        vector<int> ans;
        if (count(nums.begin(), nums.end(), val1) > n / 3)
            ans.push_back(val1);
        if (count(nums.begin(), nums.end(), val2) > n / 3 && val1 != val2)
            ans.push_back(val2);
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/majority-element-ii/
