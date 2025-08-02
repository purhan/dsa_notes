# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/139076550-9b749434-04d0-4313-8bb0-a81bbcccc981.png)

[Tutorial](https://www.youtube.com/watch?v=kSo8W6ZGYqw&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=52)

# Thought Process
- Answer is same for array and sorted array since we are dealing with subsequences and min, max of all subsequences will remain same (write on paper, think!)
- For every index in sorted array, a[i] will contribute as max for all subarrays between `1, 2, 3, 4 ... i`
- For every index in sorted array, a[i] will contribute as min for all subarrays between `i, i + 1, i + 2 ..... n`
- So, for every index, we add `a[i] * number of subarrays from 1...i`. And we subtract `a[i] * number of subarrays from i...n`

# Code
```cpp
class Solution {
public:
    int sumSubseqWidths(vector<int>& nums) {
        long long int ans = 0, n = nums.size(), mod = 1000000007;
        sort(nums.begin(), nums.end());

        vector<long long> powerOfTwo(n);                                            // ignore this code
        powerOfTwo[0] = 1;                                                          // ignore this code
        for(int i = 1; i < n; ++i) powerOfTwo[i] = (powerOfTwo[i - 1] * 2) % mod;   // ignore this code

        for(int i = 0; i < n; ++i) {
            ans += nums[i] * (powerOfTwo[i] - 1);
            ans -= nums[i] * (powerOfTwo[n - i - 1] - 1);
            ans %= mod;
        }
        return ans % mod;
    }
};
```

# Problem Links
- https://leetcode.com/problems/sum-of-subsequence-widths/
