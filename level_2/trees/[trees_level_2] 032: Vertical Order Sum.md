# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=3N4PXGyfYiI&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=32)

# Thought Process

# Code
```cpp
class Solution{
    void helper(Node* root, int x, map<int, int>& m) {
        if(!root) return;
        m[x] += (root->data);
        helper(root->left, x - 1, m);
        helper(root->right, x + 1, m);
    }
  public:
    vector <int> verticalSum(Node *root) {
        vector<int> ans;
        map<int, int> m;
        helper(root, 0, m);
        for(auto i: m) {
            ans.push_back(i.second);
        }
        return ans;
    }
};
```

# Problem Links
- https://practice.geeksforgeeks.org/problems/vertical-sum/1
