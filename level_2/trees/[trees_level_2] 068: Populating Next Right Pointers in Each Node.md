# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=3MRPQFUpoA0&list=PL-Jc9J83PIiHgjQ9wfJ8w-rXU368xNX4L&index=68)

# Thought Process
- Keep a pointer to move leve-by-level (calling it black)
- On each level, we are at the leftmost node in the starting. Connect its child nodes, then move to the next node in the same level
- So 2 while loops

# Code
```cpp
class Solution {
public:
    Node* connect(Node* root) {
        Node* black = root;

        while(black != NULL && black->left != NULL) {
            Node* curr = black;

            while(true) {
                curr->left->next = curr->right;

                if(n->next == NULL) break;
                curr->right->next = curr->next->left;
                curr = curr->next;
            }
            black = black->left;
        }
        return root;
    }
};
```

# Problem Links
- https://leetcode.com/problems/populating-next-right-pointers-in-each-node/
