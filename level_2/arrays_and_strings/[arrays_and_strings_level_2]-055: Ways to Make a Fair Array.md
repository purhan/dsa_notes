# Problem Statement
You are given an integer array nums. You can choose exactly one index (0-indexed) and remove the element. Notice that the index of the elements may change after the removal.

For example, if nums = [6,1,7,4,1]:

    Choosing to remove index 1 results in nums = [6,7,4,1].
    Choosing to remove index 2 results in nums = [6,1,4,1].
    Choosing to remove index 4 results in nums = [6,1,7,4].

An array is fair if the sum of the odd-indexed values equals the sum of the even-indexed values.

Return the number of indices that you could choose such that after the removal, nums is fair.

[Tutorial](https://www.youtube.com/watch?v=s0JtNntehsM&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=56)

# Thought Process
- For each index, if we remove that index, all even-indexed numbers on right become odd-index and vice versa, but the numbers on left of that index remain unchanged
- We can store even index and odd index sum of whole array in 2 variables
- We will traverse through the whole index, each time subtracting that element from even or odd sum depending on its own index
- Each time, we will also maintain 2 more variables which will store even-sum and odd-sum on the left of that index
- Each time, we will compare if even_left+odd_right == even_right+odd_left (since even_right and odd_right are swapping, we can just compare like this without actually swapping them)

# Code
```cpp
class Solution {
public:
    int waysToMakeFair(vector<int>& nums) {
        int n = size(nums);
        int esum_r = 0, osum_r = 0, ans = 0;
        int esum_l = 0, osum_l = 0;

        for(int i = 0; i < n; ++i) {
            if(i % 2 == 0) esum_r += nums[i];
            else osum_r += nums[i];
        }

        for(int i = 0; i < n; ++i) {
            if(i % 2 == 0) {
                esum_r -= nums[i];
                if(i > 0) osum_l += nums[i - 1];
            } else {
                osum_r -= nums[i];
                if(i > 0) esum_l += nums[i - 1];
            }
            if(esum_l + osum_r == esum_r + osum_l) ans++;
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/ways-to-make-a-fair-array/
