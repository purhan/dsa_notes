# Problem Statement

[Tutorial]()

# Thought Process

# Code
```cpp
ListNode *reverse(ListNode *head)
{

    ListNode* curr=head,*prev=nullptr,*nex=nullptr;
    while(curr){
        nex=curr->next;
        curr->next=prev;
        prev=curr;
        curr=nex;
    }
    return prev;
}
ListNode *midNode(ListNode *head)
{
    if (head == nullptr || head->next == nullptr)
        return head;

    ListNode *slow = head;
    ListNode *fast = head;
    while (fast->next != nullptr && fast->next->next != nullptr)
    {
        slow = slow->next;
        fast = fast->next->next;
    }

    return slow;
}


ListNode* singleDigitMul(ListNode* head,int a){
    ListNode* dummy=new ListNode(-1);
    ListNode* itr = dummy;

    ListNode* curr=head;
    int carry=0;

    while(curr!=NULL || carry!=0){
        int mul=carry;
        if(curr!=NULL){
            mul+=curr->val*a;
            curr=curr->next;
        }
        int val = mul%10;
        carry = mul/10;
        itr->next = new ListNode(val);
        itr=itr->next;
    }
    return dummy->next;
}

// add 2 Linkelist
void add2LL(ListNode* &l1,ListNode* &l2){

    ListNode* s2=l1;
    ListNode* s1=l2;
    int carry=0;

    while(s1->next || s2 || carry!=0){
        int sum=carry;
        if(s2!=NULL){
            sum+=s2->val;
            s2=s2->next;

        }
        if(s1->next){
            sum+=s1->next->val;

        }
        else{
            s1->next = new ListNode(0);
        }

        int val = sum%10;
        carry = sum/10;

        s1->next->val = val;
        s1=s1->next;
    }


}


// multiply 2 linkedlist
ListNode* multiply2LL(ListNode* l1,ListNode* l2){
    ListNode* dummy = new ListNode(-1);
    ListNode* itr=dummy;

    ListNode* c1=reverse(l1);
    ListNode* c2=reverse(l2);

    while(c2){
        int d = c2->val;
        c2=c2->next;

        ListNode* ptr = singleDigitMul(c1,d);

        add2LL(ptr,itr);

        itr=itr->next;
    }

    return reverse(dummy->next);
}
```

# Problem Links
