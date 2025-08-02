# Problem Statement
1. You are given an array of integers(arr) and a number K.
2. You have to find the count of subarrays whose sum is divisible by K.

[Tutorial](https://www.youtube.com/watch?v=QM0klnvTQzk&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=31)

# Thought Process
- Start traversing and calculating prefix sum at each index
- Store the `prefixSum % k` in a frequency map
- If a remainder repeats, that means that from its previous occurence to this occurence, the sum of the subarray will be divisible by k

# Code
```cpp
class Solution {
public:
    int subarraysDivByK(vector<int>& nums, int k) {
        int n = nums.size();
        int pSum = 0;
        map<int, int> sumFreq;

        int ans = 0;
        sumFreq[0] = 1;
        for(int i = 0; i < n; ++i) {
            pSum += nums[i];

            int rem = pSum % k;
            if(rem < 0) rem += k;

            ans += sumFreq[rem];
            sumFreq[rem]++;
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/subarray-sums-divisible-by-k
