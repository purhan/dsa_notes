# Problem Statement

Given an integer array nums where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.
A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

[Tutorial](https://www.youtube.com/watch?v=UAsLKuEMhsQ&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=15)

# Thought Process
- Make the middle node into the root of the tree, recursively call for the left and right subtrees

# Code
```cpp
class Solution {
    vector<int> nums;

    TreeNode* ConstructFromInorder(int si, int ei) {
        if(si > ei) return NULL;

        int mid = (si + ei) / 2;
        TreeNode* root = new TreeNode(nums[mid]);

        root->left = ConstructFromInorder(si, mid - 1);
        root->right = ConstructFromInorder(mid + 1, ei);

        return root;
    }

public:
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        this->nums = nums;
        return ConstructFromInorder(0, nums.size() - 1);
    }
};
```

# Problem Links
- Different name but same question: https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/