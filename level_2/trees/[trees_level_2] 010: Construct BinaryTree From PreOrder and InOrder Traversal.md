# Problem Statement

Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.

[Tutorial](https://www.youtube.com/watch?v=oAbSNJ35qAs&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=10)
[Striver](https://www.youtube.com/watch?v=aZNaLrVebKQ)

# Thought Process
- An observation to make: First element of preOrder is going to be the root of the whole tree
- Find the position of this element in inOrder (use hashing to speed this up)

![image](https://user-images.githubusercontent.com/10897423/145225992-a9e0cbc2-c6c3-4b76-9ae8-4cadc1f70e21.png)

- Now, the elements towards the left of this in the inOrder will be in the left subtree, and right in the right subtree
- Recursively call for the left subtree and right subtree, sending appropriate starting and ending positions as arguments

# Code
```cpp
class Solution {
    vector<int> preorder, inorder;
    map<int, int>inPos;

    TreeNode* buildTreeHelper(int pStart, int pEnd, int iStart, int iEnd) {
        if(pStart > pEnd || iStart > iEnd) return NULL;

        TreeNode* root = new TreeNode(preorder[pStart]);

        int inRoot = inPos[root->val];
        int numsLeftCnt = inRoot - iStart;

        root->left = buildTreeHelper(pStart + 1, pStart + numsLeftCnt, iStart, inRoot - 1);
        root->right = buildTreeHelper(pStart + numsLeftCnt + 1, pEnd, inRoot + 1, iEnd);

        return root;
    }
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        this->preorder = preorder, this->inorder = inorder;

        for(int i = 0; i < inorder.size(); ++i)
            this->inPos[inorder[i]] = i;

        TreeNode* root = buildTreeHelper(0, preorder.size() - 1, 0, inorder.size() - 1);

        return root;
    }
};
```

# Problem Links
- https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/
