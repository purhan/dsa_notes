# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/144709051-7d03e13c-e1f5-4640-aa48-effd67fb5b35.png)

[Tutorial](https://www.youtube.com/watch?v=8e6U4O5VUx0&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=57)

# Thought Process
- I would argue this is not even DP
- There will always be 2 possibillities
- We are given 2 lengths, lets call these a and b
- Either Subarray a is on left and subarray b is on right
- Or subarray b is on left and subarray a is on right
- We write a helper function and supply it firstLen and secondLen as a and b. We swap a and b the second time to calculate the second answer, and return the max of these
- What `helper` actually does:
- For each index, we calculate the max subarray of firstLen ending at that index
- For each index, we calculate the max subarray of second starting at that index
- For each index, we find the sum of both these values, and update the max ans

# Code
```cpp
class Solution {
    int helper(vector<int>& nums, int firstLen, int secondLen) {
        int n = nums.size();
        vector<int> dp1(n); // max ending here of length firstLen
        vector<int> dp2(n); // max ending here from the right of length secondLen

        int sum = 0;    // sum of the window ending at this index
        for(int i = 0; i < n; ++i) {
            if(i - firstLen < 0) {
                sum += nums[i];
                dp1[i] = sum;
            } else {
                sum += nums[i];
                sum -= nums[i - firstLen];
                dp1[i] = max(dp1[i - 1], sum);
            }
        }

        sum = 0;
        for(int i = n - 1; i >= 0; --i) {
            if(i + secondLen >= n) {
                sum += nums[i];
                dp2[i] = sum;
            } else {
                sum += nums[i];
                sum -= nums[i + secondLen];
                dp2[i] = max(dp2[i + 1], sum);
            }
        }

        int ans = 0;
        for(int i = firstLen - 1; i < n - secondLen; ++i) ans = max(ans, dp1[i] + dp2[i + 1]);

        return ans;
    }
public:
    int maxSumTwoNoOverlap(vector<int>& nums, int firstLen, int secondLen) {
        return max(helper(nums, firstLen, secondLen), helper(nums, secondLen, firstLen));
    }
};
```

# Problem Links
- https://leetcode.com/problems/maximum-sum-of-two-non-overlapping-subarrays/
