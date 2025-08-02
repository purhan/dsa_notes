# Problem Statement

Given the root of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

    The left subtree of a node contains only nodes with keys less than the node's key.
    The right subtree of a node contains only nodes with keys greater than the node's key.
    Both the left and right subtrees must also be binary search trees.

[Tutorial](https://www.youtube.com/watch?v=kMrbTnd5W9U&list=PL-Jc9J83PIiHYxUk8dSu2_G7MR1PaGXN4&index=50)

# Thought Process

Property of a BST:
`All values on the left of a node are smaller, all values on the right of a node are larger than that element`

Recursive:
- Check if left subtree is BST
- Check if right subtree is BST
- Some smart work required here. For every node, we want the largest value on the left, and smallest value on the right. It will be a BST only if `leftMax < currNode < rightMin`
- In the `isBST` function, we pass leftMax and rightMin. When calling left subtree, its rightMin will be our currNode. When calling right subtree, its leftMax will be our currNode.

# Code
```cpp
#define lli long long
class Solution {
    bool isBST(TreeNode* root, lli leftMax, lli rightMin) {

        if(root == NULL) return true;

        if(leftMax >= root->val || rightMin <= root->val) return false;

        return isBST(root->left, leftMax, root->val) && isBST(root->right, root->val, rightMin);
    }
public:
    bool isValidBST(TreeNode* root) {
        return isBST(root, LONG_LONG_MIN, LONG_LONG_MAX);
    }
};
```

# Problem Links
- https://leetcode.com/problems/validate-binary-search-tree/
