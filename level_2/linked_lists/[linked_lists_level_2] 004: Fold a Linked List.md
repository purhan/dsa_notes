# Problem Statement

[Tutorial]()

# Thought Process

# Code
```cpp
// midNode and reverse have to be implemented separately
void fold(ListNode *head)
{
    if(!head || !head->next){
        return;
    }
    ListNode* temp=head;
    ListNode* mid=midNode(head);
    ListNode* rev=reverse(mid);

    ListNode* cnext=nullptr,*rnext=nullptr;
    while(temp && rev){
        cnext=temp->next;
        rnext=rev->next;

        temp->next=rev;

        rev->next=cnext;

        temp=cnext;
        rev=rnext;
    }
}
```

# Problem Links
