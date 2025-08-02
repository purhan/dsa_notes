# Problem Statement

[Tutorial]()

# Thought Process

# Code
```cpp
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        ListNode* curr = head;
        while(curr) {
            while(curr->next && curr->next->val == curr->val) {
                curr->next = curr->next->next;
            }
            curr = curr->next;
        }
        return head;
    }
};
```

# Problem Links
- https://leetcode.com/problems/remove-duplicates-from-sorted-list/
