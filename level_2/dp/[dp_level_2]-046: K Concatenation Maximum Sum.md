# Problem Statement
1. You are given an array(arr1) of integers and an integer k.
2. Another array(arr2) is formed by concatenating K copies of arr1.
   For example, if arr1 = {1,2} and k = 3, then arr2 = {1,2,1,2,1,2}.
3. You have to find the maximum subarray sum in arr2.

[Tutorial](https://www.youtube.com/watch?v=qnoOu5Usb4o&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=46)

# Thought Process
- Check the code, only the `solve` function is important for revision

# Code
```cpp
int kadane(int n, vector<int> a) {
    int curr_sum = a[0];
    int ans = a[0];

    for (int i = 1; i < n; ++i) {
        if (curr_sum >= 0) {
            curr_sum += a[i];
        } else {
            curr_sum = a[i];
        }

        ans = max(curr_sum, ans);
    }

    return ans;
}

int kadaneOfTwo(int n, vector<int> a) {
    vector<int> b = a;
    for (int i = 0; i < n; ++i) b.push_back(a[i]);

    return kadane(2 * n, b);
}

void solve(int n, vector<int> a, int k) {
    if (k == 1) {
        cout << kadane(n, a);
    } else {
        int sum = accumulate(a.begin(), a.end(), 0);
        if (sum < 0) {
            cout << kadaneOfTwo(n, a);
        } else {
            cout << kadaneOfTwo(n, a) + (k - 2) * sum;
        }
    }
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/k-concatenation-official/ojquestion#!
