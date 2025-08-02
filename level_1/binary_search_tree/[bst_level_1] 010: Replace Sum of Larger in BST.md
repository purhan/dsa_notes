# Problem Statement
Given the root of a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus the sum of all keys greater than the original key in BST.

![](https://assets.leetcode.com/uploads/2019/05/02/tree.png)

Problem statement differs a little from the question. But solution is almost same. (Check leaf nodes to see the difference)

[Tutorial](https://www.youtube.com/watch?v=MLff3CxNVTc&list=PL-Jc9J83PIiGl_-iS5k7R7SZoZPt0Fab2&index=10)

# Thought Process
- Uses reverse inorder traversal (inorder -> Left-Root-Right | reverse inorder -> Right-Root-Left)
- In inorder traversal, we basically traverse in a sorted manner. So in reverse inorder, we will be traversing from largest to smallest value in the tree
- To get a GST, we just have to add the sum of all numbers larger than that number to that node
- So, we do an inorder traversal, maintain a sum, and keep adding the number to the sum. At every node, we have sum of all values larger than that node and we update the node accordingly

# Code
```cpp
class Solution {
    void helper(TreeNode* root, int& sum) {
        if(root == NULL) return;
        helper(root->right, sum);   // Right subtree

        sum += root->val;           // Root
        root->val = sum;

        helper(root->left, sum);    // Left subtree
    }
public:
    TreeNode* bstToGst(TreeNode* root) {
        int sum = 0;
        helper(root, sum);  // performs reverse inorder on the root and updates sum
        return root;
    }
};
```

# Problem Links
- https://leetcode.com/problems/binary-search-tree-to-greater-sum-tree/
