# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=VYczyMiMTqA&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=60)

# Thought Process
- Solve recursively
- Submit again for revision
- A catch here, we increment by 2 in a for loop. We have to THINK, for there to be a FULL Binary tree, there need to be an ODD number of nodes in that subtree.

# Code
```cpp
class Solution {
public:
    vector<TreeNode*> allPossibleFBT(int n) {
        vector<TreeNode*> ans;
        if(n == 1) {
            TreeNode* root = new TreeNode(0);
            ans.push_back(root);
            return ans;
        }

        for(int i = 1; i < n; i += 2) {
            vector<TreeNode*> left = allPossibleFBT(i);
            vector<TreeNode*> right = allPossibleFBT(n - i - 1);

            for(auto l: left) {
                for(auto r: right) {
                    TreeNode* root = new TreeNode(0, l, r);
                    ans.push_back(root);
                }
            }
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/all-possible-full-binary-trees/
