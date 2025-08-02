# Problem Statement
Given an unsorted array arr[] of n positive integers. Find the number of triangles that can be formed with three different array elements as lengths of three sides of triangles.

[Tutorial](https://www.youtube.com/watch?v=PqEiJDdt3S4&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=26)

# Thought Process
- Uses two pointers
- Similar to Count the Triplets problem. Code is self explanatory

# Code
```cpp
void solve(vector<int> nums, int n) {
    sort(nums.begin(), nums.end());

    int cnt = 0;

    for (int i = n - 1; i >= 2; --i) {
        int l = 0;
        int r = i - 1;

        while (l < r) {
            if (nums[l] + nums[r] > nums[i]) {
                cnt += (r - l);
                r--;
            } else {
                l++;
            }
        }
    }

    cout << cnt << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/count-possible-triangles-official/ojquestion
