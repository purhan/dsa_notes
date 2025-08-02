# Problem Statement

[Tutorial]()

# Thought Process

# Code
```cpp
ListNode *segregateOnLastIndex(ListNode *head)
{
    ListNode *sh=new ListNode(-1);  // smaller
    ListNode *gh=new ListNode(-1);  // greater

    ListNode *st=sh , *gt=gh;
    ListNode* pivot=getTail(head);
    int data=pivot->val;
    ListNode* curr=head;
    while(curr){
        if(curr->val <= data){
            st->next=curr;
            st=st->next;
        }
        else{
            gt->next=curr;
            gt=gt->next;
        }
        curr=curr->next;
    }

    st->next=gh->next;
    gt->next=nullptr;
    return st;
}
```

# Problem Links
