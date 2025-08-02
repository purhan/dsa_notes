# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/138100878-33a4b2f7-fced-4604-8f8d-63b56f77dd6b.png)

[Tutorial](https://www.youtube.com/watch?v=qUDp8IUbZto&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=3)

# Thought Process

Must be done in O(N)

- Create two pointers i, j at start, end
- whichever height is smaller (a[i] or a[j]), move that pointer
- take max of all those areas

Intuition behind this:
- Moving to the next pillar takes 1 distance no matter what
- So if we were to look for another pillar, we should move the pointer at the smaller pillar only

# Code
```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int n = size(height);
        int i = 0, j = n - 1;

        int ans = 0;
        while(i < j) {
            ans = max(ans, (j - i) * min(height[i], height[j]));

            if(height[i] > height[j]) j--;
            else i++;
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/container-with-most-water/
