# Problem Statement
You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.


[Tutorial](https://www.youtube.com/watch?v=tCVOQX3lWeI&list=PL-Jc9J83PIiEyUGT3S8zPdTMYojwZPLUM&index=15)

# Thought Process

# Code
```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> nextGreater(n);

        // Store index of next greater element
        stack<int> s;
        for(int i = n - 1; i >= 0; --i) {
            while(!s.empty() && nums[s.top()] <= nums[i]) {
                s.pop();
            }

            if(s.empty()) nextGreater[i] = n;
            else nextGreater[i] = s.top();

            s.push(i);
        }

        // For each window, the element whose NGE is outside this window, is the largest element in this window
        vector<int> ans;
        int j = 0;
        for(int i = 0; i <= n - k; ++i) {
            if(j < i) j = i;
            while(nextGreater[j] < i + k) {
                j++;
            }

            ans.push_back(nums[j]);
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/sliding-window-maximum/