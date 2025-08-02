# Problem Statement
1. You are provided with marks of N students in Physics, Chemistry and Maths.
Perform the following 3 operations:
a). Sort the students in Ascending order of their Physics marks.
b). Once this is done, sort the students having same marks in Physics in the descending order of their Chemistry marks.
c). Once this is also done, sort the students having same marks in Physics and Chemistry in the ascending order of their Maths marks.
2. Your task is to complete the function customSort() which takes  phy[],  chem[],  math[] . The function sorts the marks in the described order and the final changes should be made in the given arrays only.

[Tutorial](https://www.youtube.com/watch?v=aGMzcfWsdWE&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq)

# Thought Process
- Just write a custom comparator

# Code
```cpp
bool comp(const vector<int> a, const vector<int> b) {
    if (a[0] == b[0]) {
        if (a[1] == b[1]) {
            return a[2] < b[2];
        } else {
            return a[1] > b[1];
        }
    } else {
        return a[0] < b[0];
    }
}

void solve(vector<vector<int>> marks) {
    sort(marks.begin(), marks.end(), comp);
    for (auto i : marks) {
        cout << i[0] << " " << i[1] << " " << i[2] << endl;
    }
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/marks_of_pcm/ojquestion#!
