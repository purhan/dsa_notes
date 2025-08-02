# Problem Statement

[Tutorial]()

# Thought Process

Iterative:
- Do a BFS and find 2 nodes with maximum level, return their levels' sum

Recursive:
- Diameter is always height of LST + height of RST
- For each level, we can calculate HLST+HRST and return the max of it
- We can optimize by passing diameter as a reference in the height function itself

# Code
```cpp
// More intuitive
class Solution {
    int height(TreeNode* root) {
        if(root == NULL) return 0;
        return max(height(root->left), height(root->right)) + 1;
    }
public:
    int diameterOfBinaryTree(TreeNode* root) {
        if(root == NULL) return 0;
        int lh = height(root->left);
        int rh = height(root->right);
        return max({lh + rh, diameterOfBinaryTree(root->left), diameterOfBinaryTree(root->right)});
    }
};

// Optimized
class Solution {
    int height(TreeNode* root, int &diameter) {
        if(root == NULL) return 0;
        int lh = height(root->left, diameter);
        int rh = height(root->right, diameter);
        diameter = max(diameter, lh + rh);
        return max(lh, rh) + 1;
    }
public:
    int diameterOfBinaryTree(TreeNode* root) {
        int diameter = 0;
        height(root, diameter);
        return diameter;
    }
};
```

# Problem Links
