# Problem Statement

[Tutorial]()

# Thought Process

# Code
```cpp
// recursive
ListNode *mergeTwoLists(ListNode *l1, ListNode *l2)
{
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

// iterative
ListNode *mergeTwoLists(ListNode *l1, ListNode *l2)
{
    if(!l1){
        return l2;
    }
    if(!l2){
        return l1;
    }

    ListNode* dm = new ListNode(-1); //dummy
    ListNode* ansH = dm;
    ListNode* p1 = l1;
    ListNode* p2 = l2;

    while(p1 != NULL && p2 != NULL) {
        if(p1->val <= p2->val) {
            dm->next = p1;
            p1 = p1->next;
            dm = dm->next;
        }
        else {
            dm->next = p2;
            p2 = p2->next;
            dm = dm->next;
        }
    }

    if(p1 != NULL) {
        dm->next = p1;
    }

    if(p2 != NULL) {
        dm->next = p2;
    }

    return ansH->next;
}
```

# Problem Links
