# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/144714566-9b9f4d3d-3fe5-485b-bad4-23fc03511c13.png)

[Tutorial](https://www.youtube.com/watch?v=rSi4MpGEz1M&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=60)

# Thought Process
- Traverse linearly and at every point, check length of current running AP
- Add this length to answer everytime to include all subarrays of this subarray
- Reset count when an AP breaks

# Code
```cpp
class Solution {
public:
    int numberOfArithmeticSlices(vector<int>& nums) {
        int ans = 0, cur = 0;
        for(int i = 2; i < nums.size(); ++i) {
            if(nums[i] - nums[i - 1] == nums[i - 1] - nums[i - 2]) {    // if this element is in AP with previous pair
                cur++;                                                  // then increment length of current AP
                ans += cur;                                             // Add curr to answer to include ALL subsets of curr
            } else {
                cur = 0;                                                // reset curr when an AP breaks
            }
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/arithmetic-slices/
