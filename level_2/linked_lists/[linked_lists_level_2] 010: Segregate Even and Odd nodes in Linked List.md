# Problem Statement

[Tutorial]()

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/136373666-9f1786e5-c0c1-4210-bade-18d176484fb9.png)

# Code
```cpp
ListNode *segregateEvenOdd(ListNode *head)
{
    ListNode* even=new ListNode(-1);
    ListNode* odd=new ListNode(-1);
    ListNode* d1=even,*d2=odd;

    ListNode* temp=head;
    while(temp){
        if(temp->val%2==0){
            d1->next=temp;
            d1=d1->next;
            temp=temp->next;
        }
        else{
            d2->next=temp;
            d2=d2->next;
            temp=temp->next;
        }

    }
    d1->next=odd->next;
    d2->next=nullptr;
    return even->next;
}
```

# Problem Links
