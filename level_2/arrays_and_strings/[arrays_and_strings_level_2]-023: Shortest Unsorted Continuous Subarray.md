# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138308576-fb5d494a-4169-4012-9202-15ed88593e5c.png)

[Tutorial](https://www.youtube.com/watch?v=GvAtQOMr8CQ&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=23)

# Thought Process
- In the array, we have to check how much of the array in the begining and at the end is correct (as it should be in sorted array). We will NOT sort our array for this however.

![image](https://user-images.githubusercontent.com/10897423/138308996-85dc3be3-ac85-4893-80f0-36b86ea1aa90.png)

- We will maintain leftMax and rightMin for range query arrays
- From left, we will check how many elements satisfy -> `a[i] < rightMin[i+1] && a[i] > leftMax[i-1]`. When this condition fails, we break out of the loop
  - This tells us, that till that index all elements are correct
- From right, we will check how many elements satisfy -> `a[i] > rightMin[i+1] && a[i] > leftMax[i-1]`. When this condition fails, we break out of the loop
  - This tells us, that till that index all elements are correct

All the remaining un-traversed elements have to be sorted, so their cnt is our answer

# Code
```cpp
class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        int n = nums.size();
        vector<int> leftMax(n, INT_MIN), rightMin(n, INT_MAX);

        // calculate leftMax and rightMin for each index
        for(int i = 0; i < n; ++i) {
            if(i > 0) leftMax[i] = leftMax[i - 1];
            leftMax[i] = max(leftMax[i], nums[i]);
        }
        for(int i = n - 1; i >= 0; --i) {
            if(i < n - 1) rightMin[i] = rightMin[i + 1];
            rightMin[i] = min(rightMin[i], nums[i]);
        }

        // On left and right ends of the array, count numbers that satisfy our condition
        int cnt = 0;
        for(int i = 0; i < n; ++i) {
            if(i > 0 && nums[i] < leftMax[i - 1]) break;
            if(i < n - 1 && nums[i] > rightMin[i + 1]) break;
            cnt++;
        }
        for(int i = n - 1; i >= 0; --i) {
            if(i < n - 1 && nums[i] > rightMin[i + 1]) break;
            if(i > 0 && nums[i] < leftMax[i - 1]) break;
            cnt++;
        }

        // Return count of remaining elements
        return max(0, n - cnt);
    }
};
```

# Problem Links
- https://leetcode.com/problems/shortest-unsorted-continuous-subarray/
