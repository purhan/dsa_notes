# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=x9wAMfcGI8A&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=63)

# Thought Process
- Use BFS
- If a node in queue has both children, just pop it
- If a node is missing on of the children, insert new node below this one, and add both its children in the queue

# Code
```cpp
class CBTInserter {
    TreeNode* globalroot;
    queue<TreeNode*> q;
public:
    CBTInserter(TreeNode* root) {
        this->globalroot = root;

        this->q.push(root);
    }

    int insert(int val) {
        TreeNode* node = new TreeNode(val);
        while(true) {
            auto f = q.front();
            if(f->left != NULL && f->right != NULL) q.pop();
            if(f->left != NULL) q.push(f->left);
            if(f->right != NULL) q.push(f->right);

            if(f->left == NULL) {
                f->left = node;
                q.push(node);
                return f->val;
            } else if(f->right == NULL) {
                f->right = node;
                q.push(node);
                return f->val;
            }
        }
    }

    TreeNode* get_root() {
        return this->globalroot;
    }
};
```

# Problem Links
- https://leetcode.com/problems/complete-binary-tree-inserter/
