# Problem Statement

Given an array of integers preorder, which represents the preorder traversal of a BST (i.e., binary search tree), construct the tree and return its root.

[Tutorial](https://www.youtube.com/watch?v=Bexswo4pqZQ&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=16)

# Thought Process
- Code is self explanatory, recursive
- I'd recommend re-solving to revise
- Approach:
- Recursively collect BST for a given left range and right range, and attatch that to this root

# Code
```cpp
class Solution {
    vector<int> preorder;
    int idx = 0;

    TreeNode* getBst(int lr, int rr) { // index, left range (smaller), right range (greater)
        if(idx >= preorder.size() || preorder[idx] < lr || preorder[idx] > rr) return NULL;

        TreeNode* root = new TreeNode(preorder[idx]);
        idx++;

        root->left = getBst(lr, root->val);
        root->right = getBst(root->val, rr);

        return root;
    }

public:
    TreeNode* bstFromPreorder(vector<int>& preorder) {
        this->preorder = preorder;
        return getBst(INT_MIN, INT_MAX);
    }
};
```

# Problem Links
- https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/
