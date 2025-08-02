# Problem Statement
1. You are given two integer arrays(A and B), where B is an anagram of A.
2. B is an anagram of A means B is made by randomizing the order of the elements in A.
3. For every element in A, you have to print the index of that element in B.

[Tutorial](https://www.youtube.com/watch?v=jBkTf43X198&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=21)

# Thought Process
- Store all positions from `b` in a `map<int, array>`
- Traverse through `a` and print top value from map's array, and pop that value since its now printed already

# Code
```cpp
void solve(vector<int> a, vector<int> b, int n) {
    map<int, queue<int>> positions;

    for (int i = 0; i < n; ++i) {
        positions[b[i]].push(i);
    }

    for (int i = 0; i < n; ++i) {
        int pos = positions[a[i]].front();
        positions[a[i]].pop();
        cout << pos << " ";
    }
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/hashmap-and-heaps/find-anagram-mappings-official/ojquestion
