# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138552515-dbf9761b-1d6c-450d-8696-fb63835bda74.png)

[Tutorial](https://www.youtube.com/watch?v=LfB2tkmsrCA&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=43)

# Thought Process
- This solution covers 2Sum, 3Sum, 4Sum and kSum

First, understand how 2sum works:
- Sort the array, start 2 pointers from left and right, and count the pairs for which `nums[l]+nums[r] = target`
- For unique pairs, skip left pointer on repeating values

Now, understand how 3sum works:
- Sort the array, start a pointer from left. Now, check for all 2sum pairs in the remaining array with `target = target-nums[l]`

Now, understand how 4sum works:
- Sort the array, start a pointer from left. Now, check for all 3sum pairs in the remaining array with `target = target-nums[l]`

kSum is just a continuation of this strategy

- I would recommend **solving** this problem again and not just reading the code during revision

# Code
```cpp
class Solution {

    vector<vector<int>> twoSum(vector<int>& nums, int target, int si) {
        int n = size(nums);
        vector<vector<int>> res;
        if(n - si < 2) return res;

        int l = si, r = n - 1;
        while(l < r) {
            if(l != si && nums[l] == nums[l - 1]) {
                l++;
                continue;
            }
            int sum = nums[l] + nums[r];
            if(sum == target) {
                vector<int> subRes = {nums[l], nums[r]};
                res.push_back(subRes);

                l++;
                r--;
            } else if(sum > target) {
                r--;
            } else {
                l++;
            }
        }
        return res;
    }

    vector<vector<int>> kSum(vector<int>& nums, int target, int si, int k) {
        int n = size(nums);
        if(k == 2) {
            return twoSum(nums, target, si);
        }

        vector<vector<int>> res;
        if(n - si < k) return res;

        // Traverse pointer from left to right, and solve for k-1Sum in the remaining array
        for(int i = si; i < n; ++i) {
            if(i != si && nums[i] == nums[i - 1]) continue; // we are ignoring duplicate values for this problem

            int val = nums[i];
            // solve for k-1Sum
            auto subRes = kSum(nums, target - val, i + 1, k - 1);
            for(auto v: subRes) {
                // Add THIS pointer into the k-1Sum result, and add that to our result
                v.push_back(val);
                res.push_back(v);
            }
        }
        return res;
    }

public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());
        return kSum(nums, target, 0, 4);
    }
};
```

# Problem Links
- https://leetcode.com/problems/4sum/
