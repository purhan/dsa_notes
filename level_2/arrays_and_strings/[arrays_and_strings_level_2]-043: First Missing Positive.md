# Problem Statement
Given an unsorted integer array nums, return the smallest missing positive integer.

You must implement an algorithm that runs in O(n) time and uses constant extra space.

[Tutorial](https://www.youtube.com/watch?v=QeBvfH1dpOU&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=43)

# Thought Process
- Question tells us to do in O(1) space, but we will do in O(n) space first for understanding.

- If we were to assume that, the array contains only numbers `1, 2, 3, 4, .... n-1`, then the ans is `n`
- Ans can be at most n. Or else, some number between `1, 2, 3, 4, .... n-1` would be missing and would be ans
- So, first we traverse through array and get rid of (mark as 0) the numbers that are out of range [1, n].
- Now, in a hashmap, we will store which numbers are remaining.
- Finally, we will check the hashmap (for 1..n only). If a number is missing from hashmap, it's the ans. Else, the ans is `n`

Without using hashmap:
- We can smartly use the original array as a hashmap

# Code

Using hashmap:
```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        nums.push_back(0);  // just to prevent the case nums=[1]. We would lose `1` since 1==n in this case
        int n = size(nums);

        // Number must be in range [1, n). If all numbers in [1,n) are present, then `n` will be ans
        // Get rid of all numbers that are out of range
        for(int i = 0; i < n; ++i) {
            if(nums[i] < 0 || nums[i] >= n) nums[i] = 0;
        }

        // Using hashmap to keep track of present numbers
        map<int, bool> isPresent;
        for(int i = 0; i < n; ++i) {
            isPresent[nums[i]] = true;
        }

        // If number not in hashmap, return it
        for(int i = 1; i < n; ++i) {
            if(!isPresent[i]) return i;
        }

        // If all numbers in [1,n) were in array, `n` is the next smallest number. So return that
        return n;
    }
};
```

Without hashmap:
```cpp
class Solution {
public:
    int firstMissingPositive(vector<int>& nums) {
        nums.push_back(0);  // just to prevent the case nums=[1]. We would lose `1` since 1==n in this case
        int n = size(nums);

        // Number must be in range [1, n). If all numbers in [1,n) are present, then `n` will be ans
        // Get rid of all numbers that are out of range
        for(int i = 0; i < n; ++i) {
            if(nums[i] < 0 || nums[i] >= n) nums[i] = 0;
        }

        // Smart trick to use input array as hashmap
        for(int i = 0; i < n; ++i) {
            nums[nums[i]%n] += n;
        }

        // If number not in hashmap, return it
        for(int i = 0; i < n; ++i) {
            if(nums[i] / n == 0) return i;
        }

        // If all numbers in [1,n) were in array, `n` is the next smallest number. So return that
        return n;
    }
};
```

# Problem Links
- https://leetcode.com/problems/first-missing-positive/
