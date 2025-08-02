# Problem Statement

[Tutorial]()

# Thought Process

# Code
```cpp
void unfold(ListNode *head)
{
    if(!head || !head->next){
        return;
    }
    ListNode* l1=head;
    ListNode* l2=head->next;
    ListNode* p1=l1,*p2=l2;

    while(p1->next && p2->next){
        ListNode* n1=p1->next;
        ListNode* n2=p2->next;

        p1->next=n2;
        p2->next=n2->next;

        p1=p1->next;
        p2=p2->next;
    }

    l2=reverse(l2);
    p1->next=l2;
}
```

# Problem Links
