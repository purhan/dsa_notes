# Problem Statement
Given a binary array nums, return the maximum length of a contiguous subarray with an equal number of 0 and 1.

[Tutorial](https://www.youtube.com/watch?v=1WugaISSWx8&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=34)

# Thought Process
- We start traversing from left to right and store the count of 0's and 1's till that index
- Whenever we reach a point where, if the difference between `count0 - count1` repeats at two indexes, that means that the subarray between those two indeces has `count0 = count1`

To implement in code, we dont actually need to store both counts separately and we only need to store the difference between count0 and count1

Doing that is simple, Only take count of `1's` and subtract from the count whenever a 0 is found

# Code
```cpp
class Solution {
public:
    int findMaxLength(vector<int>& nums) {
        int n = nums.size(), ans = 0;
        int cnt = 0;
        map<int, int> firstOccurenceOfDiff;

        firstOccurenceOfDiff[0] = -1;   // This is for the case when a subarray from index 0->x satisfies the condition
        for(int i = 0; i < n; ++i) {
            if(nums[i] == 1) cnt++;
            else cnt--;

            if(firstOccurenceOfDiff.find(cnt) != firstOccurenceOfDiff.end()) {
                ans = max(ans, i - firstOccurenceOfDiff[cnt]);
            } else {
                firstOccurenceOfDiff[cnt] = i;
            }
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/contiguous-array/
