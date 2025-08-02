# Problem Statement
1. You are given an array of integers(arr) and a number K.
2. You have to find the count of subarrays whose sum equals k.

[Tutorial](https://www.youtube.com/watch?v=20v8zSo2v18&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=28)

# Thought Process
- Create a hashmap of prefix sum
- Start traversing and creating a prefixSum array (or use a single int for the same purpose)
- Everytime, lookup if a subarray had prefixSum == `currPrefixSum - k`
- Add all such subarrays to ans
- Store currPrefixSum in the hashmap for upcoming lookups

# Code
```cpp
class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        int n = nums.size();
        int psum = 0;           // Prefix sum frequency array (dont need an array so just using this int)
        map<int, int> sumFreq;  // Sores frequency of elements in the prefix sum
        sumFreq[0] = 1;

        int ans = 0;
        for(int i = 0; i < n; ++i) {
            psum += nums[i];
            ans += sumFreq[psum - k];
            sumFreq[psum]++;
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/subarray-sum-equals-k/
