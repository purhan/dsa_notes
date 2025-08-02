# Problem Statement
1. You are given an array(arr) which contains only 0's and 1's and a number K.
2. You have to find the maximum number of consecutive 1's in the given array if you can flip at most K zeroes.

[Tutorial](https://www.youtube.com/watch?v=QPfalDbqa4A&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=15)

# Thought Process
- Uses acquire release strategy
- We start with two pointers, start acquiring numbers till we have acquired less than or equal to `k` zeroes
- Whenever we acquire more than k zeroes, we start releasing from the left until we have k zeroes again, then we continue acquiring again and so on
- We take max length of all such valid subarrays formed during this process

# Code
```cpp
class Solution {
public:
    int longestOnes(vector<int>& nums, int k) {
        int n = size(nums);

        int ans = 0;
        int zeroCnt = 0;
        int l = 0;

        for(int r = 0; r < n; ++r) {
            if(nums[r] == 0) {
                zeroCnt++;
            }

            while(zeroCnt > k) {
                if(nums[l] == 0) zeroCnt--;
                l++;
            }

            ans = max(ans, r - l + 1);
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/max-consecutive-ones-iii
