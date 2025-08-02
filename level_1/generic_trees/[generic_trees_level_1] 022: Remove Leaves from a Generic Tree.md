# Problem Statement

[Tutorial]()

# Thought Process
- Solve Recursively

# Code
```cpp
// doesnt exist on leetcode, but heres some code for referenceclass Solution {
public:
    TreeNode* removeLeafNodes(TreeNode* root) {
        if (root->left) root->left = removeLeafNodes(root->left);
        if (root->right) root->right = removeLeafNodes(root->right);

        // If both left and right are null, its leaf so remove it (return null)
        // Else, return it normally
        return (root->left == root->right && root->right == nullptr) ? nullptr : root;
    }
};
```

# Problem Links
