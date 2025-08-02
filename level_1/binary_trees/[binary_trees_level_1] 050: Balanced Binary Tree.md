# Problem Statement
Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

    a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

[Tutorial](https://www.youtube.com/watch?v=9X1TYiipolA&list=PL-Jc9J83PIiHYxUk8dSu2_G7MR1PaGXN4&index=50)

# Thought Process
Property of a balanced BT:

difference of height between any two subtrees <= 1

- Recursively, we will calculate height of every subtree
- At every node, we will call for height of left subtree and right subtree
- We will maintain a global variable isBalanced
- For every node, we will compare height of left subtree and right subtree and update isBalanced = false if condition is ever not satisfied

# Code
```cpp
class Solution {
    int height(TreeNode* root, bool& isBalanced) {
        if(root == NULL) return 0;

        int lh = height(root->left, isBalanced);
        int rh = height(root->right, isBalanced);
        if(abs(lh - rh) > 1) isBalanced = false;
        return max(lh, rh) + 1;
    }
public:
    bool isBalanced(TreeNode* root) {
        bool res = true;
        height(root, res);
        return res;
    }
};
```

# Problem Links
- https://leetcode.com/problems/balanced-binary-tree/
