# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=qzdTHpuP434&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=19)

# Thought Process

- **REVISE THE IMPLEMENTATION, SPECIALLY THE STRINGSTREAM PART**

# Code
```cpp
class Codec {
    int idx = 0;

    TreeNode* vectorToTree(vector<string> &v) {
        if(v[idx] == "NULL") {
            idx++;
            return NULL;
        } else {
            TreeNode* node = new TreeNode(stoi(v[idx]));
            idx++;
            node->left = vectorToTree(v);
            node->right = vectorToTree(v);
            return node;
        }
    }

public:

    string serialize(TreeNode* root) {
        if(root == NULL) return "NULL";

        string left = serialize(root->left);
        string right = serialize(root->right);

        return to_string(root->val) + " " + left + " " + right;
    }

    TreeNode* deserialize(string data) {
        vector<string> v;
        stringstream ss(data);
        string word;

        while(ss >> word) {
            v.push_back(word);
        }

        this->idx = 0;
        return vectorToTree(v);
    }
};
```

# Problem Links
- https://leetcode.com/problems/serialize-and-deserialize-binary-tree/
