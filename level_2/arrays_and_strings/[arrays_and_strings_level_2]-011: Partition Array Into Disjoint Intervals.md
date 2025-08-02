# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138224338-4b8a8350-40c4-403a-a60d-d79bc77c639c.png)

[Tutorial](https://www.youtube.com/watch?v=FRG2YlZdmPE&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=11)

# Thought Process

> This uses O(n) space. Pending solution for O(1) space

- Condition for a valid partition -> `min value on right > max value on left`
- For each index, store min on right and max on left
- Return first such index where `min value on right > max value on left`

# Code
```cpp
class Solution {
public:
    int partitionDisjoint(vector<int>& nums) {
        int n = size(nums);

        // Store min on the right of each index
        vector<int> minFromRight(n);
        int mn = INT_MAX;
        for(int i = n - 1; i >= 0; --i) {
            mn = min(mn, nums[i]);
            minFromRight[i] = mn;
        }

        // Store max on the left of each index
        // We have ans if all values on `right` are greater than all values on `left`
        // So just compare *max on left* and *min on right*
        int maxFromLeft = -1;
        for(int i = 0; i < n - 1; ++i) {
            maxFromLeft = max(maxFromLeft, nums[i]);
            if(maxFromLeft <= minFromRight[i + 1]) {
                return i + 1;
            }
        }

        return n - 1;
    }
};
```

# Problem Links
- https://leetcode.com/problems/partition-array-into-disjoint-intervals/
