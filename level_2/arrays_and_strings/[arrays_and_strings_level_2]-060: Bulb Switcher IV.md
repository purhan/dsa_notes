# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/139433597-f047ccdf-b8ac-4a87-8fcc-1df2aaadc27c.png)

[Tutorial](https://www.youtube.com/watch?v=VGDHph1k0tQ&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=60)

# Thought Process
- I would like you to "think"! first!!

- SPOILER: reverse engineer it
- Start from an empty array (all elements 0). To turn this into the resultant array, we traverse from left to right, and whenever indeces dont match, we flip the array to the right of it

# Code
```cpp
class Solution {
public:
    int minFlips(string target) {
        char curr = '0';
        int ans = 0;

        for(int i = 0; i < target.size(); ++i) {
            if(target[i] == curr) continue;
            else {
                ans++;
                curr = target[i];
            }
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/bulb-switcher-iv/
