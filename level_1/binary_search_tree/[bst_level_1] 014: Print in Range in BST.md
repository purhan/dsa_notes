# Problem Statement
Given the root node of a binary search tree and two integers low and high, return the sum of values of all nodes with a value in the inclusive range [low, high].

[Tutorial](https://www.youtube.com/watch?v=NEJUsqEFOI4&list=PL-Jc9J83PIiGl_-iS5k7R7SZoZPt0Fab2&index=14)

# Thought Process
- Perform inorder and update the sum
- If, we go out of range, we don't need to continue inorder in that particular part of the tree. Inspect the code carefully

# Code
```cpp
class Solution {
    void helper(TreeNode* root, int low, int high, int& sum) {
        if(root == NULL) return;

        // inorder -> left-root-right

        if(root->val >= low)
            helper(root->left, low, high, sum);                     // if still in range, call left subtree

        if(root->val >= low && root->val <= high)
            sum += root->val;                                       // add current value to sum if in range

        if(root->val <= high)
            helper(root->right, low, high, sum);                    // if still in range, call right subtree
    }
public:
    int rangeSumBST(TreeNode* root, int low, int high) {
        int sum = 0;
        helper(root, low, high, sum);   // inorder traversal, but don't traverse nodes that are out of lo-hi range
        return sum;
    }
};
```

# Problem Links

