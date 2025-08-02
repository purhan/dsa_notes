# Problem Statement
1. You are given a list of lists, where each list is sorted.
2. You are required to complete the body of mergeKSortedLists function. The function is expected to merge k sorted lists to create one sorted list.

OR

You are given an array of k linked-lists lists, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

[Tutorial](https://www.youtube.com/watch?v=E5WSILx1q0Q&list=PL-Jc9J83PIiHq5rMZasunIR19QG3E-PAA&index=20)
[Leetcode Article](https://leetcode.com/problems/merge-k-sorted-lists/discuss/850425/simple-cpp-priority-queue-solution)

# Thought Process
- Create a priority queue `pq` of size equal to number of lists
- Pop the first node `Node* t` from `pq` and push `t->next` into `pq`
- Repeat popping nodes and pushing their `next` into `pq`
- Return the list of all the popped nodes

# Code
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    struct compare {
        bool operator()(ListNode* &a, ListNode* &b) {
            return a->val > b->val;
        }
    };

    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<ListNode*, vector<ListNode*>, compare> pq;
        for(int i = 0; i < (int)size(lists); ++i) {
            if(lists[i] != NULL) pq.push(lists[i]);
        }

        ListNode* head = new ListNode(0);
        ListNode* curr = head;

        while(!pq.empty()) {
            auto t = pq.top();
            pq.pop();

            curr->next = t;
            curr = curr->next;

            if(t->next != NULL) pq.push(t->next);
        }

        return head->next;
    }
};
```

# Problem Links
- https://www.pepcoding.com/resources/online-java-foundation/hashmap-and-heap/merge-k-sorted-lists-official/ojquestion
- https://leetcode.com/problems/merge-k-sorted-lists/
