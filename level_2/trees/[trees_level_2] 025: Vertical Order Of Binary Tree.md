# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=LscPXvD1N1A&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=25)

# Thought Process
- This code below is complicated because of leetcode's weird demands, but the approach is extremely simple
- Do a level order traversal, for each node, add +1 or -1 depending on whether its on left or right (let's call this its x coordinate)
- In a map, store the nodes for each x coordinate (`map<x, vector<Node>>`)

- **We can optimize sorting part using Priority Queue as explained in** https://www.youtube.com/watch?v=8o-0CxZHNdQ&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=33

# Code
```cpp
class Solution {
public:
    static bool comp(const pair<int, int>& a, const pair<int, int>& b) {
        if(a.second == b.second) {
            return a.first < b.first;
        }
        return a.second < b.second;
    }

    vector<vector<int>> verticalTraversal(TreeNode* root) {
        vector<vector<int>> ans;
        map<int, vector<pair<int, int>>> m;
        queue<pair<TreeNode*, pair<int, int>>> q;

        q.push({root, {0, 0}});

        while(!q.empty()) {
            auto f = q.front();
            q.pop();
            if(f.first == NULL) continue;
            m[f.second.first].push_back({f.first->val, f.second.second});
            q.push({f.first->left, {f.second.first - 1, f.second.second + 1}});
            q.push({f.first->right, {f.second.first + 1, f.second.second + 1}});
        }

        for(auto [x, y]: m) {
            sort(y.begin(), y.end(), comp);
            vector<int> a;
            for(auto k: y)
                a.push_back(k.first);
            ans.push_back(a);
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/
