# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/144445116-9ad9121b-ba1e-4cc7-8616-e6e51afdc80d.png)

[Tutorial](https://www.youtube.com/watch?v=7aqHhENUbkQ&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=10)

# Thought Process
- Tutorial used slightly different approach but intuition was same

- Run a DFS. Each time, carry last direction in parameters. If last direction was left, this time we can go right and increment `answer so far`, or go left again and start from 1. And so on.

# Code
```cpp
class Solution {
public:
    int ans;

    void dfs(TreeNode* root, bool dir, int anssf) { // dir true = left, false = right
        if(!root) return;
        ans = max(ans, anssf);

        if(dir) {
            dfs(root->left, false, anssf + 1);
            dfs(root->right, true, 1);
        } else {
            dfs(root->left, false, 1);
            dfs(root->right, true, anssf + 1);
        }
    }

    int longestZigZag(TreeNode* root) {
        ans = 0;
        dfs(root, true, 0);
        dfs(root, false, 0);
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/longest-zigzag-path-in-a-binary-tree/
