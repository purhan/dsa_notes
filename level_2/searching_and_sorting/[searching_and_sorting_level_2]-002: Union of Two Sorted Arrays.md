# Problem Statement
1. Given two sorted arrays a[] and b[] of size n and m respectively. The task is to find union between these two arrays.
2. Union of the two arrays can be defined as the set containing distinct elements from both the arrays. If there are repetitions, then only one occurrence of element should be printed in union.
3. Your task is to complete Union function that takes a, b as parameters and returns an Arraylist which contains the union elements of the two arrays.The printing is done by the driver code.

[Tutorial](https://www.youtube.com/watch?v=JCT04Z94Nyo&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=2)

# Thought Process
- Put 2 pointers on the first elements of both arrays `A` and `B`
- Keep increasing pointer on `A` and putting that element into the new array `C` while comparing with `B`. In case element in `B` is smaller, activate `B`'s pointer and continue the process with that
- Since we need to find union, numbers shouldn't repeat. So only push_back into `C` if the last element of `C` is different, and won't repeat this time.

# Code
```cpp
void solve(vector<int> a, vector<int> b, int n, int m) {
    int i = 0, j = 0;
    vector<int> c;
    while (i < n || j < m) {
        if (a[i] == b[j]) {
            if (c.size()) {
                if (c.back() != a[i])
                    c.push_back(a[i]);
            } else {
                c.push_back(a[i]);
            }
            i++;
            j++;
        } else if (a[i] < b[j]) {
            if (c.size()) {
                if (c.back() != a[i])
                    c.push_back(a[i]);
            } else {
                c.push_back(a[i]);
            }
            i++;
        } else {
            if (c.size()) {
                if (c.back() != b[j])
                    c.push_back(b[j]);
            } else {
                c.push_back(b[j]);
            }
            j++;
        }
    }
    if (i == n) {
        while (j != m) {
            c.push_back(b[j]);
            j++;
        }
    } else if (j == m) {
        while (i != n) {
            c.push_back(a[i]);
            i++;
        }
    }
    for (auto k : c) {
        cout << k << " ";
    }
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/union_of_two_sorted_arrays/ojquestion
