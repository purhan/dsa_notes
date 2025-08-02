# Problem Statement

You are given the root of a binary tree. We install cameras on the tree nodes where each camera at a node can monitor its parent, itself, and its immediate children.

Return the minimum number of cameras needed to monitor all nodes of the tree.

[Tutorial](https://www.youtube.com/watch?v=uoFrIIrp5_g&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=5)

# Thought Process
- Dont think of a DP solution just yet!
- We create a new function, `needCamera` which asks its children if they need a camera
- it returns a flag with the following possible values

    1  : It's covered by either its child ~~or parent~~

    0  : It has a camera itself

    -1 : It isn't covered, so parent needs to provide a camera

- Based on the value, if children return -1, we increment answer by 1, and return 0 indicating we set up a camera at this node
- If children return 0, we need not do anything, and return 1 as this node is already covered
- If children return 1, it means they are covered by their children, but this node is not covered, so we return -1. It's better to make the parent use a camera always, rather than its child (greedy approach)

# Code
```cpp
class Solution {
    int cameras;

    int needCamera(TreeNode* root) {
        if(root == NULL) return 1;

        int lchild = needCamera(root->left);
        int rchild = needCamera(root->right);

        if(lchild == -1 || rchild == -1) {
            cameras++;
            return 0;
        } else if(lchild == 0 || rchild == 0) {
            return 1;
        } else {
            return -1;
        }
    }
public:
    int minCameraCover(TreeNode* root) {
        cameras = 0;    // careful, this is a global var
        if(needCamera(root) == -1) cameras++;
        return cameras;
    }
};
```

# Problem Links
- https://leetcode.com/problems/binary-tree-cameras/
