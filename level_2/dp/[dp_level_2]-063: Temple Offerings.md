# Problem Statement

1. Pepcoder is wishing to give offerings to all the temples along a mountain range. 

2. The temples are located in a row at different heights.

3. You have to find the minimum number of offerings such that these conditions are fulfilled - 

    -> If two adjacent temples are at different heights, then the temple which is situated at greater height should receive more offerings.

    -> If two adjacent temples are at the same height, then their offerings relative to each other does not matter.   

[Tutorial](https://www.youtube.com/watch?v=q40s16m5FD0&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=63)

# Thought Process
- A local maximum has to be bigger than both the temples on the left as well as the ones on the right
- First, we set values for left strokes only. We traverse from left to right and if it is increasing, we give them values accordingly (one bigger than previous)
- Then we traverse in reverse and do the same in reverse
- The values on peaks (local maxima) are now maximum of the ones from left and right, since it has to satisfy both

# Code
```cpp
void solve(int n, vector<int> nums) {
    int ans = 0;
    vector<int> left(n);
    left[0] = 1;
    vector<int> right(n);
    right[n - 1] = 1;

    for (int i = 1; i < n; ++i) {
        if (nums[i] > nums[i - 1]) {
            left[i] = left[i - 1] + 1;
        } else {
            left[i] = 1;
        }
    }

    for (int i = n - 2; i >= 0; --i) {
        if (nums[i] > nums[i + 1]) {
            right[i] = right[i + 1] + 1;
        } else {
            right[i] = 1;
        }
    }

    for (int i = 0; i < n; ++i) ans += max(left[i], right[i]);

    cout << ans << endl;
}
```

# Problem Links
- https://nados.pepcoding.com/content/eb9863ac-63ac-4b94-881f-0aeb24df0985/0c54b191-7b99-4f2c-acb3-e7f2ec748b2a/7fdb0602-0ac9-4484-aff9-a898aed5cd28/f74cfd53-06b7-402e-9065-3f84ef402395/5539a6e8-c8bf-4f04-805c-e43e9d20e72a/question/3083a439-4154-4843-aa37-6a4550f9394d
