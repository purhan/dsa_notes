# Problem Statement
Given a sorted array of size N. Count the number of distinct absolute values present in the array.

[Tutorial](https://www.youtube.com/watch?v=9M0asQIYy0Q&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=32)

# Thought Process
- Concept is easy, code is complicated
- Uses two pointer method

# Code
```cpp
void solve(vector<int> nums, int n) {
    int i = 0, j = n - 1;
    int cnt = 0;
    int prev = INT_MIN, next = INT_MAX;

    while (i <= j) {
        if (abs(nums[i]) == abs(nums[j])) {
            if (nums[i] != prev && nums[j] != next) {
                cnt++;
            }
            prev = nums[i];
            next = nums[j];
            j--;
            i++;
        } else if (abs(nums[i]) < abs(nums[j])) {
            if (nums[j] != next) {
                cnt++;
            }
            next = nums[j];
            j--;
        } else {
            if (nums[i] != prev) {
                cnt++;
            }
            prev = nums[i];
            i++;
        }
    }
    cout << cnt << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/distinct-absolute-array-elements-official/ojquestion#!
