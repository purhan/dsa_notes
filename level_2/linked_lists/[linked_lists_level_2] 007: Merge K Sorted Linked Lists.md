# Problem Statement

[Tutorial]()

# Thought Process

> Very Important: Also read divide and conquer method and priority queue method

- Merge pairs of lists one-by-one

# Code
```cpp
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


ListNode *mergeKLists(vector<ListNode *> &lists)
{
    ListNode* temp=lists[0];
    for(int i=1;i<lists.size();i++){
        ListNode* te=mergeTwoLists(temp,lists[i]);
        temp=te;
    }
    return temp;
}
```

# Problem Links
