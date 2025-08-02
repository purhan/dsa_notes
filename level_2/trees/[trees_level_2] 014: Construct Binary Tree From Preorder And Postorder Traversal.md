# Problem Statement

Given two integer arrays, preorder and postorder where preorder is the preorder traversal of a binary tree of distinct values and postorder is the postorder traversal of the same tree, reconstruct and return the binary tree.

[Tutorial](https://www.youtube.com/watch?v=xe6cLIhberQ&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=15)

# Thought Process
- Similar to previous 2, but the key difference here is that we need root as well as one child to move forward in the algorithm

# Code
```cpp
class Solution {
    vector<int> preorder, postorder;
    map<int, int> postPos;

    TreeNode* constructHelper(int preStart, int preEnd, int postStart, int postEnd) {
        if(preStart > preEnd || postStart > postEnd) return NULL;

        // First element in preOrder is the root
        // Find index of root in postOrder. If nothing after root, just return root
        TreeNode* root = new TreeNode(preorder[preStart]);
        if(preStart == preEnd) return root;

        // In preorder, node next to root is its child. In postorder, the ones left to child are its children, and towards right are not its children
        TreeNode* child = new TreeNode(preorder[preStart + 1]);
        int childIdx = postPos[child->val];
        int leftRem = childIdx - postStart + 1;

        root->left = constructHelper(preStart + 1, preStart + leftRem, postStart, childIdx);
        root->right = constructHelper(preStart + leftRem + 1, preEnd, childIdx + 1, postEnd);

        return root;
    }

public:
    TreeNode* constructFromPrePost(vector<int>& preorder, vector<int>& postorder) {
        this->preorder = preorder;
        this->postorder = postorder;

        for(int i = 0; i < postorder.size(); ++i)
            postPos[postorder[i]] = i;

        return constructHelper(0, preorder.size() - 1, 0, postorder.size() - 1);
    }
};
```

# Problem Links
- https://leetcode.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/
