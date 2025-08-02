# Problem Statement

The thief has found himself a new place for his thievery again. There is only one entrance to this area, called root.

Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that all houses in this place form a binary tree. It will automatically contact the police if two directly-linked houses were broken into on the same night.

Given the root of the binary tree, return the maximum amount of money the thief can rob without alerting the police.

[Tutorial](https://www.youtube.com/watch?v=kTL5LhCTL1c&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=6)

# Thought Process
- Simple include exclude principle. May be different from tutorial, I was able to solve on my own

# Code
```cpp
class Solution {
public:
    unordered_map<TreeNode*, int> mem;
    int rob(TreeNode* root) {
        if(root == NULL) return 0;

        if(mem[root]) return mem[root];

        // if robbed at this node
        int robbed = root->val;
        // just to avoid nullptr exception. Imagine all this on one line only!
        if(root->right) robbed += rob(root->right->right) + rob(root->right->left);
        if(root->left) robbed += rob(root->left->right) + rob(root->left->left);

        // if skipped this node
        int skipped = rob(root->right) + rob(root->left);

        return mem[root] = max(robbed, skipped);
    }
};
```

# Problem Links
- https://leetcode.com/problems/house-robber-iii
