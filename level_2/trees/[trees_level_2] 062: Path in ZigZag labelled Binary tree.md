# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/147071306-ba7126d6-c3a7-4cc0-8cc1-82a4cfc9d3d8.png)

[Tutorial](https://www.youtube.com/watch?v=2Hn_dhDbHRE&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=63)

# Thought Process
- The tree formed is almost same as a normal tree, the difference being, nodes at odd levels are reversed
- In a normal tree, the parent of a node is always `n / 2`
- In the tree we have, the parent of a node is always `complement[n] / 2`
- `complement[n] = n` for even levels
- `complement[n] = something else` for odd levels (look at the code and screenshot)

# Code
```cpp
class Solution {
public:
    vector<int> pathInZigZagTree(int n) {
        int power = 1, i = 0;
        while(i < n) {
            i += power;
            power *= 2;
        }
        power /= 2;

        vector<int> ans;

        while(n > 1) {
            ans.push_back(n);
            int complement = (3 * power - n - 1);
            int parent = complement / 2;
            n = parent;
            power /= 2;
        }
        ans.push_back(1);

        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/path-in-zigzag-labelled-binary-tree/
