# Problem Statement
Given the root of a binary tree, the value of a target node target, and an integer k, return an array of the values of all nodes that have a distance k from the target node.

You can return the answer in any order.

![image](https://user-images.githubusercontent.com/10897423/137633444-ef408dbc-659b-40e4-ad4e-5bab00298860.png)

[Tutorial](https://www.youtube.com/watch?v=B89In5BctFA&list=PL-Jc9J83PIiHYxUk8dSu2_G7MR1PaGXN4&index=26)

# Thought Process
- Store node-to-root path in an array
- For every element in the path, print k-down of that element, reducing k each time
- **Patiently read this step as well**. Keep a map of elements that are already on the path, since we don't want to go k-down from an element and print another element that's on the path already. Because it will not be k-far from our target.
- So, just don't add such nodes in the BFS queue

We are making use of 2 **important** functions, which will be explained here only:

Get Node to root path
- This works recursively
- Keep a global variable for `path`
- Check left subtree and right subtree, if a subtree doesn't contain the target, it will return NULL, so do nothing in this case
- If a subtree returned something other than NULL, add current node to path

Print K Down
- Initialize a BFS from the root node, keep a track of current level, and whenever level == k, print those nodes


# Code
```cpp
class Solution {
    TreeNode* getNodeToRootPath(TreeNode* root, TreeNode* target, vector<TreeNode*>& psf) {
        if(root == NULL) return root;
        if(root == target) {
            psf.push_back(root);
            return root;
        }
        auto l = getNodeToRootPath(root->left, target, psf);
        auto r = getNodeToRootPath(root->right, target, psf);

        if(l != NULL || r != NULL) {
            psf.push_back(root);
            return root;
        } else
            return NULL;
    }

    void printKDown(TreeNode* root, int k, vector<int>& ans, unordered_map<TreeNode*, bool>& onPath) {
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()) {
            int level_size = q.size();
            while(level_size--) {
                auto rem = q.front();
                q.pop();

                if(rem->left && !onPath[rem->left]) q.push(rem->left);
                if(rem->right && !onPath[rem->right]) q.push(rem->right);
            }
            k--;
            if(!k) break;
        }
        while(!q.empty()) {
            auto rem = q.front();
            q.pop();
            ans.push_back(rem->val);
        }
    }

public:
    vector<int> distanceK(TreeNode* root, TreeNode* target, int k) {
        vector<int> ans;
        vector<TreeNode*> node_to_root;
        unordered_map<TreeNode*, bool> onPath;
        getNodeToRootPath(root, target, node_to_root);

        for(auto i: node_to_root) onPath[i] = true;

        for(auto i: node_to_root) {
            if(k == 0) {
                ans.push_back(i->val);
                break;
            }
            printKDown(i, k, ans, onPath);
            k--;
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/
