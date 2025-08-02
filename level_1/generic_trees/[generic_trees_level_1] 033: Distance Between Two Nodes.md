# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=5N5tpizDXys&list=PL-Jc9J83PIiEmjuIVDrwR9h5i9TT2CEU_&index=33)

# Thought Process

# Code
```cpp
#include <bits/stdc++.h>
using namespace std;
struct Node
{
    int data;
    vector<Node *> children;
};

Node *construct(int *arr, int n)
{
    Node *root = new Node();
    root->data = arr[0];
    stack<Node *> st;
    st.push(root);

    for (int i = 1; i < n; i++)
    {
        if (arr[i] == -1)
        {
            st.pop();
        }
        else
        {
            Node *nn = new Node();
            nn->data = arr[i];
            st.top()->children.push_back(nn);
            st.push(nn);
        }
    }
    return root;
}

vector<Node *> nodetorootpath(Node *root, int data)
{
    if (root == nullptr)
    {
        vector<Node *> n;
        return n;
    }

    if (root->data == data)
    {
        vector<Node *> nn;
        nn.push_back(root);
        return nn;
    }

    for (int i = 0; i < root->children.size(); i++)
    {
        vector<Node *> res = nodetorootpath(root->children[i], data);
        if (res.size() > 0)
        {
            res.push_back(root);
            return res;
        }
    }
    vector<Node *> s;
    return s;
}

void lowestcommanancestor(Node *root, int a, int b)
{
    if (root == nullptr)
    {
        return;
    }
    vector<Node *> ans1 = nodetorootpath(root, a);
    vector<Node *> ans2 = nodetorootpath(root, b);
    int i = ans1.size() - 1, j = ans2.size() - 1;
    Node *lca = ans1[i];
    while (i >= 0 && j >= 0)
    {
        if (ans1[i]->data != ans2[j]->data)
        {
            break;
        }
        lca = ans1[i];
        i--;
        j--;
    }

    vector<Node *> lca2a = nodetorootpath(lca, a);
    vector<Node *> lca2b = nodetorootpath(lca, b);
    cout << lca2a.size() - 1 + lca2b.size() - 1;
}

int main()
{
    int n;
    cin >> n;
    int arr[n];
    for (int i = 0; i < n; i++)
    {
        cin >> arr[i];
    }
    int a, b;
    cin >> a >> b;
    Node *root = construct(arr, n);
    lowestcommanancestor(root, a, b);
    return 0;
}
```

# Problem Links
