# Problem Statement

[Tutorial]()

# Thought Process

# Code
```cpp
class Solution {
    Node* getNodeToRootPath(Node* root, int target, vector<Node*>& psf) {
        if(root == NULL) return root;
        if(root->data == target) {
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
    void getMaxDepth(Node* root, int dsf, int& ans, map<Node*, bool>& visited) {
        if(!root) return;
        if(visited[root]) return;
        visited[root] = true;

        ans = max(ans, dsf);

        getMaxDepth(root->left, dsf + 1, ans, visited);
        getMaxDepth(root->right, dsf + 1, ans, visited);
    }
  public:
    int minTime(Node* root, int target) 
    {
        // Your code goes here
        vector<Node*> nrp;
        getNodeToRootPath(root, target, nrp);
        map<Node*, bool> visited;
        int ans = 0;

        for(int i = 0; i < nrp.size(); ++i) {
            getMaxDepth(nrp[i], i, ans, visited);
        }
        return ans;
    }
};
```

# Problem Links
- https://practice.geeksforgeeks.org/problems/burning-tree/1/?category[]=Tree&category[]=Tree&page=5&query=category[]Treepage5category[]Tree#
