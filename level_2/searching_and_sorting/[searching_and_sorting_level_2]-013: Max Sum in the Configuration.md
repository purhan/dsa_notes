# Problem Statement
1. Given an array, you have to find the max sum of i*A[i] where A[i] is the element at index i in the array.
2. The only operation allowed is to rotate(clock-wise or counter clock-wise) the array any number of times.

[Tutorial](https://www.youtube.com/watch?v=yroWfS5P2E4&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=14)

# Thought Process

![image](https://user-images.githubusercontent.com/10897423/134799979-161a0c03-ed99-45cd-bfb7-cfed8b586c10.png)

![image](https://user-images.githubusercontent.com/10897423/134799985-c7c65dc1-bfdc-4d72-9fbe-e8c7df8fede7.png)

- Come up with the formula in the screenshot
- Watch tutorial for how to derive this formula

# Code

```cpp
void solve(vector<int> nums, int n) {
    int sum = 0, s0 = 0;

    for (int i = 0; i < n; ++i) {
        sum += nums[i];
        s0 += nums[i] * i;
    }

    int mx = s0;
    int si = s0;

    for (int i = 0; i < n - 1; ++i) {
        si = si + sum - n * nums[n - i - 1];
        mx = max(mx, si);
    }

    cout << mx << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/max-sum-in-the-configuration/ojquestion
