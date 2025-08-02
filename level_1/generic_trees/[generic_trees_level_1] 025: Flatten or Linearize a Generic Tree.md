# Problem Statement

[Tutorial]()

Striver did a better video on this

# Thought Process

# Code

> Solving this for Binary Tree. Can be solved for generic trees too

Recursive

```cpp
class Solution {
    TreeNode* prev = NULL;
public:
    void flatten(TreeNode* root) {
        if(root == NULL) return;

        flatten(root->right);
        flatten(root->left);

        root->right = prev;
        root->left = NULL;
        prev = root;
    }
};
```

Iterative

```cpp
class Solution {
public:
    void flatten(TreeNode* root) {
        if(root == NULL) return;
        stack<TreeNode*> st;
        st.push(root);

        while(!st.empty()) {
            TreeNode* cur = st.top();
            st.pop();

            if(cur->right != NULL) st.push(cur->right);
            if(cur->left != NULL) st.push(cur->left);

            if(!st.empty()) {
                cur->right = st.top();
            }
            cur->left = NULL;
        }
    }
};
```

# Problem Links

\* not for generic trees

- https://leetcode.com/problems/flatten-binary-tree-to-linked-list
