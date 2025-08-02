# Problem Statement

Given an array nums of size n, return the majority element.

The majority element is the element that appears more than ⌊n / 2⌋ times. You may assume that the majority element always exists in the array.

[Tutorial](https://www.youtube.com/watch?v=3tbjwaGC-ng&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=6)

# Thought Process
- Uses Boyer-Moore Voting Algorithm
- Whenever we get a certain amount of votes (count) for a candidate, that becomes our top candidate
- Whenever that candidate repeats, its votes increase. If another candidate/element appears in the array, it eats up the top candidate's votes
- We start increasing count for an element. As long as its count remains >0, it remains our top candidate, else the last candidate we saw before cnt==0, that new candidate becomes our top candidate

# Code
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int n = size(nums);
        int val = 0, cnt = 0;

        for(int i = 0; i < n; ++i) {
            if(cnt == 0) {
                val = nums[i];
                cnt = 1;
            } else if(nums[i] == val) {
                cnt++;
            } else {
                cnt--;
            }
        }

        return val;
    }
};
```

# Problem Links
- https://leetcode.com/problems/majority-element/
