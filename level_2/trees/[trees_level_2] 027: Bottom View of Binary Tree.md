# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=kCQJTAqbExg&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=27)

# Thought Process

- Same for top view also

- Do a traversal, each time store its x coordinate. Print the last node for each x coordinate

# Code
```cpp
class Solution {
  public:
    vector <int> bottomView(Node *root) {
        map<int, int> m;
        queue<pair<Node*, int>> q;
        q.push({root, 0});
        vector<int> ans;

        while(!q.empty()) {
            Node* f = q.front().first;
            int x = q.front().second;
            q.pop();

            m[x] = f->data;
            if(f->left != NULL) q.push({f->left, x - 1});
            if(f->right != NULL) q.push({f->right, x + 1});
        }
        for(auto x: m) {
            ans.push_back(x.second);
        }
        return ans;
    }
};
```

# Problem Links
- https://practice.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1
