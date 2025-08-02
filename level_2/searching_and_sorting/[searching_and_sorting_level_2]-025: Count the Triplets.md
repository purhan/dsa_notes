# Problem Statement
Given an array of distinct integers. The task is to count all the triplets such that sum of two elements equals the third element

[Tutorial](https://www.youtube.com/watch?v=YnEHFYwQwyU&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=25)

# Thought Process
- Solve with Two Pointer Method. Code is easy.

# Code
```cpp
void solve(vector<int> nums, int n) {
    sort(nums.begin(), nums.end());

    int cnt = 0;

    for (int i = n - 1; i >= 2; --i) {
        int l = 0;
        int r = i - 1;

        while (l < r) {
            if (nums[l] + nums[r] == nums[i]) {
                cnt++;
                l++;
                r--;
            } else if (nums[l] + nums[r] < nums[i]) {
                l++;
            } else {
                r--;
            }
        }
    }

    cout << cnt << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/count-the-triplets-official/ojquestion
