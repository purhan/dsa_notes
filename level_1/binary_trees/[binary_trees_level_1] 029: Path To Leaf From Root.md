# Problem Statement
Given the root of a binary tree, return all root-to-leaf paths in any order.

A leaf is a node with no children.

[Tutorial](https://www.youtube.com/watch?v=A6Z5YvsrDtg&list=PL-Jc9J83PIiHYxUk8dSu2_G7MR1PaGXN4&index=29)

# Thought Process

# Code
```cpp
class Solution {
public:
    vector<string> binaryTreePaths(TreeNode* root) {
        if(root == NULL) return vector<string>(0);
        if(root->left == NULL && root->right == NULL)
            return vector<string>(1, to_string(root->val));

        vector<string> res;
        for(auto ls: binaryTreePaths(root->left)) {
            res.push_back(to_string(root->val) + "->" + ls);
        }
        for(auto rs: binaryTreePaths(root->right)) {
            res.push_back(to_string(root->val) + "->" + rs);
        }

        return res;
    }
};
```

# Problem Links
- https://leetcode.com/problems/binary-tree-paths/
