# Problem Statement
1. Given a singly linklist, Segregate 01 Node of LinkedList and return pivot node of linkedlist.
2. After segregation zero nodes should come first and followed by ones node.

[Tutorial]()

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/136795104-90044e16-dfac-43ca-8471-30f5cb0d6ab7.png)

# Code
```cpp
ListNode* segregate01(ListNode* head) {
    ListNode *dummyz(NULL), *dummyo(NULL);
    ListNode *lastz(NULL), *lasto(NULL);
    ListNode* curr = head;

    while (curr) {
        if (curr->val == 0) {
            if (dummyz == NULL) {
                dummyz = lastz = curr;
                curr = curr->next;
            } else {
                lastz->next = curr;
                lastz = lastz->next;
                curr = curr->next;
            }
        } else {
            if (dummyo == NULL) {
                dummyo = lasto = curr;
                curr = curr->next;
            } else {
                lasto->next = curr;
                lasto = lasto->next;
                curr = curr->next;
            }
        }
    }
    lasto->next = NULL;
    lastz->next = dummyo->next;
    return dummyz;
}
```

# Problem Links
