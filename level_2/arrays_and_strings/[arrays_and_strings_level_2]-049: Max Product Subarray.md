# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=jzQ-f2uU0UU&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=49)

# Thought Process
- You've gotta come up to the conclusion that the subarray either starts from the left or ends at the right of the array (Why? Look at the screenshot/tutorial, and read ahead)

![image](https://user-images.githubusercontent.com/10897423/138824512-77577dfc-f55f-4e57-bdca-48f564d5f550.png)

- For any subarray in the middle, the following cases are possible:

- `left +ve | middle +ve | right +ve` : just whole array will give max anyway
- `left +ve | middle -ve | right +ve` : either left or right will give max since middle is -ve

- `left -ve | middle +ve | right +ve` : only middle\*right (basically ending at right) will give max
- `left -ve | middle -ve | right +ve` : either left\*middle (basically starting from left) or right alone

- `left +ve | middle +ve | right -ve` : only left\*middle (basically starting from left) will give max
- `left +ve | middle -ve | right -ve` : either right\*middle (basically ending at right) or left alone will give max

- `left -ve | middle +ve | right -ve` : only middle will give max
- `left -ve | middle -ve | right -ve` : either right\*middle or left\*middle will give max

# Code
```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        int ans = INT_MIN;

        int curr = 1;
        for(int i = 0; i < nums.size(); ++i) {
            curr *= nums[i];
            ans = max(ans, curr);
            if(curr == 0) curr = 1;
        }

        curr = 1;
        for(int i = nums.size() - 1; i >= 0; --i) {
            curr *= nums[i];
            ans = max(ans, curr);
            if(curr == 0) curr = 1;
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/maximum-product-subarray/
