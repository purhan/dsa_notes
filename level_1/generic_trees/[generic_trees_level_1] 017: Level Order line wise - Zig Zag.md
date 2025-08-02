# Problem Statement

Given the root of a binary tree, return the zigzag level order traversal of its nodes' values. (i.e., from left to right, then right to left for the next level and alternate between).

[Tutorial]()

Striver had a better video on this

[LC article](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/discuss/174644/c%2B%2B-Easy-to-understand-one-approach-to-solve-Zigzag-and-Level-order-traversal)

# Thought Process
- Create a Queue
- Do a level order traversal
- At each level, create a vector
- If odd level, insert queue elements in vector normally
- If even level, insert queue elements in vector in reverse
- Print vector at the end of level

# Code
```cpp
class Solution {
public:
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        if (!root) return {};

        queue<TreeNode*> q;
        vector<vector<int>> out;

        q.push(root);
        bool dir = 0; /* to alternate levels, or a bool variable */

        while (!q.empty()) {

            int sz = q.size();
            vector<int> currLevel(sz);

            for (int i = 0; i < sz; i++) {

                TreeNode* tmp = q.front();
                q.pop();

                if (dir == 0) {
                    currLevel[i] = tmp->val; // odd level, insert like 0, 1, 2, 3 etc.
                } else {
                    currLevel[sz - i - 1] = tmp->val; /* even level insert from end. 3, 2, 1, 0. (sz - i - 1) to get the index from end */
                }

                if (tmp->left) q.push(tmp->left);
                if (tmp->right) q.push(tmp->right);
            }
            out.push_back(currLevel); // now push the level traversed to output vector
            dir = !dir;
        }
        return out;
    }
};
```

# Problem Links
- https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/
