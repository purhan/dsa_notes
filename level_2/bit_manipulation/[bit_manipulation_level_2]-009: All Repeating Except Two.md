# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=pnx5JA9LNM4&list=PL-Jc9J83PIiFJRioti3ZV7QabwoJK6eKe&index=9)

# Thought Process
- Take XOR of all elements
- In the end, we have XOR of two non repeating elements
- Surely, this XOR's bits will be different in both numbers
- We categorize all numbers of the array in 2 categories, depending on the rightmost setbit of the obtained XOR
- XOR of both categories will give us both the required numbers

# Code
```cpp
class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        int xorr = 0;
        for(auto i: nums) xorr ^= i;

        int rsb = xorr & -(long long)xorr;

        vector<int> ans(2);
        for(int i = 0; i < nums.size(); ++i) {
            if(nums[i] & rsb)
                ans[0] ^= nums[i];
            else
                ans[1] ^= nums[i];
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/single-number-iii/
