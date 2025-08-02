# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138218717-ab978732-7414-47a3-a0e9-06552976a153.png)

[Tutorial](https://www.youtube.com/watch?v=UBkpyXgx0g0&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=9)

# Thought Process
- Calculate prefix product
- Calculate suffix product
- For each index, answer will be `pre[i-1] * suff[i+1]`

# Code
```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = size(nums);
        vector<int> pre(n, 1), suff(n, 1), res(n);

        // calculate prefix product and suffix product
        for(int i = 0; i < n; ++i) {
            pre[i] *= nums[i];
            if(i > 0) pre[i] *= pre[i - 1];
        }
        for(int i = n - 1; i >= 0; --i) {
            suff[i] *= nums[i];
            if(i < n - 1) suff[i] *= suff[i + 1];
        }

        for(int i = 0; i < n; ++i) {
            if(i == 0) {
                res[i] = suff[i + 1];
            } else if(i == n - 1) {
                res[i] = pre[i - 1];
            } else {
                res[i] = pre[i - 1] * suff[i + 1];
            }
        }

        return res;
    }
};
```

# Problem Links
- https://leetcode.com/problems/product-of-array-except-self/
