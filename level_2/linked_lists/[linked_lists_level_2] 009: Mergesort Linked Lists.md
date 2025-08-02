# Problem Statement

[Tutorial]()

# Thought Process

# Code
```cpp
class ListNode {
public:
    int val = 0;
    ListNode *next = nullptr;

    ListNode(int val)
    {
        this->val = val;
    }
};

ListNode *mergeTwoLists(ListNode *l1, ListNode *l2) {
    if(!l1){
        return l2;
    }
    if(!l2){
        return l1;
    }

    if(l1->val < l2->val){
        l1->next=mergeTwoLists(l1->next,l2);
        return l1;
    }
    else{
        l2->next=mergeTwoLists(l1,l2->next);
        return l2;
    }
}

ListNode *midNode(ListNode *head) {
    ListNode* slow=head , *fast=head;
    while(fast && fast->next && fast->next->next){
        slow=slow->next;
        fast=fast->next->next;
    }
    return slow;
}

ListNode *mergeSort(ListNode *head) {
    if(!head || !head->next){
        return head;
    }

    ListNode* firsthalf=head;
    ListNode* mid = midNode(head);
    ListNode* secondHalf = mid->next;
    mid->next=nullptr;

    return mergeTwoLists(mergeSort(firsthalf),mergeSort(secondHalf));
}
```

# Problem Links
