# Problem Statement

Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.

[Tutorial](https://www.youtube.com/watch?v=XLFGcZxn0PM&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=12)
[Striver](https://www.youtube.com/watch?v=ZWGW7FminDM)

# Thought Process

Todo: using morris traversal

Striver method without using morris traversal:

- Inorder traversal of a BST gives us a sorted array
- If two nodes are swapped, it will reflect in the inorder traversal

- There can be two possibilities:
    - Two adjacent nodes were swapped
    - Two non-adjacent nodes were swapped
- We will maintain two variables `firstViolation` and `secondViolation`
- In the inorder, if we come across two numbers, where second number is not greater than the previous, this is a violation. If this is our first such occurence, we will assign `firstViolation` and `secondViolation` to these nodes implying that these two nodes were possibly adjacent and swapped
- If we encounter such occurence again (we will check by seeing if `firstViolation` is null) then we reassign `secondViolation` (think why not reassign firstViolation)

![image](https://user-images.githubusercontent.com/10897423/145196444-989cc5e5-5f04-4885-9ebb-d890c484d6b9.png)

![image](https://user-images.githubusercontent.com/10897423/145196413-29a13c3c-c1cd-439a-af14-7bbff7a7196f.png)

# Code
```cpp
class Solution {
    TreeNode* firstViolation;
    TreeNode* secondViolation;
    TreeNode* prev;

    void inorder(TreeNode* root) {
        if(root == NULL) return;

        inorder(root->left);

        if(prev != NULL && (root->val < prev->val)) {

            if(!firstViolation) {
                firstViolation = prev;
                secondViolation = root;
            }

            else
                secondViolation = root;
        }

        prev = root;
        inorder(root->right);
    }
public:
    void recoverTree(TreeNode* root) {
        inorder(root);
        swap(firstViolation->val, secondViolation->val);
    }
};
```

# Problem Links
- https://leetcode.com/problems/recover-binary-search-tree/
