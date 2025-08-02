# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=BmpXMtA0oF8&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=64)

# Thought Process
- Store nodes to be deleted in map to speed up the algo
- Just run a traversal and delete nodes
- Resubmit for revision

# Code
```cpp
class Solution {
    unordered_map<int, bool> to_remove;
    vector<TreeNode*> ans;

    TreeNode* helper(TreeNode* root) {
        if(root == NULL) return NULL;

        root->left = helper(root->left);
        root->right = helper(root->right);

        if(to_remove[root->val]) {
            if(root->left != NULL) ans.push_back(root->left);
            if(root->right != NULL) ans.push_back(root->right);
            return NULL;
        }
        return root;
    }
public:
    vector<TreeNode*> delNodes(TreeNode* root, vector<int>& to_delete) {
        for(auto i: to_delete) this->to_remove[i] = true;

        helper(root);
        if(to_remove[root->val] != true) ans.push_back(root);
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/delete-nodes-and-return-forest/
