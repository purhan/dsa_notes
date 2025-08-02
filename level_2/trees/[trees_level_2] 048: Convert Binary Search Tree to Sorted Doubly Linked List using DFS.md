# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=WBsNE_DWk9U&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=48)

# Thought Process
- This method used DFS. Check other methods in the playlis too!!!!!

# Code
```cpp
class Solution
{
    Node* ans = NULL, *prev;
    void helper(Node* root) {
        if(!root) return;
        helper(root->left);
        if(ans == NULL) {
            ans = root;
            prev = ans;
        } else {
            prev->right = root;
            prev->right->left = prev;
            prev = prev->right;
        }
        helper(root->right);
    }

public:
    Node * bToDLL(Node *root)
    {
        if(!root) return root;
        helper(root);
        return ans;
    }
};
```

# Problem Links
- https://practice.geeksforgeeks.org/problems/binary-tree-to-dll/1#
