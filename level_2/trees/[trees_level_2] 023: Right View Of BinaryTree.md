# Problem Statement

[Tutorial]()

# Thought Process
- Same as previous

# Code
```cpp
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int> ans;

        queue<TreeNode*> q;
        q.push(root);

        while(!q.empty()) {
            int level_size = q.size();
            for(int i = 0; i < level_size; ++i) {
                TreeNode* cur = q.front(); q.pop();
                if(cur == NULL) continue;
                if(i == level_size - 1) ans.push_back(cur->val);

                if(cur->left != NULL)
                    q.push(cur->left);
                if(cur->right != NULL)
                    q.push(cur->right);
            }
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/binary-tree-right-side-view/
