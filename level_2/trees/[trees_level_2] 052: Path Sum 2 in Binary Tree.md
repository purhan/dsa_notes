# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=ojxo9QjPKvA&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=53)

# Thought Process
- Simple backtracking approach

# Code
```cpp
class Solution {
    vector<vector<int>> ans;
    vector<int> psf;

    void helper(TreeNode* root, int targetSum) {
        if(!root) return;

        if(root->left == NULL && root->right == NULL && (targetSum - root->val == 0)) {
            psf.push_back(root->val);
            ans.push_back(psf);
            psf.pop_back();
            return;
        }

        psf.push_back(root->val);
        helper(root->left, targetSum - root->val);
        helper(root->right, targetSum - root->val);
        psf.pop_back();
    }
public:
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        helper(root, targetSum);
        return this->ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/path-sum-ii/
