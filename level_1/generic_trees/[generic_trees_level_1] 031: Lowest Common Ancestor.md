# Problem Statement

[Tutorial (bruteforce)](https://www.youtube.com/watch?v=w8rr1AYMlfw&list=PL-Jc9J83PIiEmjuIVDrwR9h5i9TT2CEU_&index=31)

[Striver's Tutorial (optimized)](https://www.youtube.com/watch?v=_-QHfMDde90)

# Thought Process

Bruteforce:
- Find path from Node to root for both nodes, using DFS
- Compare the paths and return the last common value

Optimized:
- Uses recursion
- Check if LCA exists on left subtree
- Check if LCA exists on right subtree
    - If Left subtree returns NULL, means `neither p nor q exist on left subtree`
    - If Right subtree returns NULL, means `neither p nor q exist on right subtree`
    - If both Left subtree and Right subtree return `something other than NULL`, it means one returned p, other returned q. So the root of this tree is LCA
    - If one tree returned NULL, other returned something else, it means LCA is somewhere in that other subtree and has already been found

# Code

Code only for optimized approach

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == NULL || root == p || root == q) return root;

        auto left = lowestCommonAncestor(root->left, p, q);
        auto right = lowestCommonAncestor(root->right, p, q);

        if(left == NULL) {          // p or q or LCA not found in Left, so right's LCA is the ans
            return right;
        } else if(right == NULL) {  // p or q or LCA found in Right, so left's LCA is the ans
            return left;
        } else {
            return root;            // p and q found on both directions, so root is ans
        }
    }
};
```

# Problem Links
