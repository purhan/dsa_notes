# Problem Statement

Given two integer arrays inorder and postorder where inorder is the inorder traversal of a binary tree and postorder is the postorder traversal of the same tree, construct and return the binary tree.

[Tutorial](https://www.youtube.com/watch?v=Lc3RBGtyn7M&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=11)

# Thought Process
- SAME as the previous one, just in reverse

# Code
```cpp
class Solution {
    vector<int> inorder, postorder;
    map<int, int> inPos;

    TreeNode* buildTreeHelper(int postStart, int postEnd, int inStart, int inEnd) {
        if(postStart > postEnd || inStart > inEnd) return NULL;

        TreeNode* root = new TreeNode(postorder[postEnd]);

        int rootPos = inPos[root->val];
        int rightRemaining = inEnd - rootPos;

        root->left = buildTreeHelper(postStart, postEnd - rightRemaining - 1, inStart, rootPos - 1);
        root->right = buildTreeHelper(postEnd - rightRemaining - 1, postEnd - 1, rootPos + 1, inEnd);

        return root;
    }
public:
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        this->postorder = postorder;
        this->inorder = inorder;

        for(int i = 0; i < inorder.size(); ++i) inPos[inorder[i]] = i;

        return buildTreeHelper(0, postorder.size() - 1, 0, inorder.size() - 1);
    }
};
```

# Problem Links
- https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/
