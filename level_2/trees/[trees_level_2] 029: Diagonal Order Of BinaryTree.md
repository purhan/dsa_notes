# Problem Statement

Given a Binary Tree, print the diagonal traversal of the binary tree.

Consider lines of slope -1 passing between nodes. Given a Binary Tree, print all diagonal elements in a binary tree belonging to same line.

[Tutorial](https://www.youtube.com/watch?v=cvK3Sb6zJ1k&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=29)

# Thought Process
- Traverse on a diagonal, and add its left children to the queue
- This adds the next diagonal to the queue to be executed next
- Most importantly, read code

# Code
```cpp
vector<int> diagonal(Node *root) {
   vector<int> ans;

   queue<Node*> q;
   q.push(root);

   while(!q.empty()) {
       Node* f = q.front(); q.pop();

       while(f != NULL) {
           ans.push_back(f->data);
           if(f->left != NULL) q.push(f->left);
           f = f->right;
       }
   }

   return ans;
}
```

# Problem Links
- https://practice.geeksforgeeks.org/problems/diagonal-traversal-of-binary-tree/1
