# Problem Statement
1. You are given an array(arr) of integers.
2. You have to find maximum subarray sum in the given array.
3. The subarray must have at least one element.

[Tutorial](https://www.youtube.com/watch?v=VMtyGnNcdPw&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=45)

# Thought Process
- Traverse through the array
- Store the `current sum` in an integer
- If the `current sum` ever becomes negative, that means:
  - The `current index` has a negative number
  - Thus, any subsequence till that number will surely be negative
  - So we reset our `current sum` at the next index
- We just take the max of all values of `current sum` throughout the traversal

> In an interview, you could solve this with prefix sum just to kill time. Prefix sum uses O(n) time and O(n) space while Kadane takes O(n) time and O(1) space.

# Code
```cpp
void solve(int n, vector<int> a) {
    int curr_sum = a[0], ans = a[0];

    for (int i = 1; i < n; ++i) {
        if (curr_sum >= 0) {
            curr_sum += a[i];
        } else {
            curr_sum = a[i];
        }

        ans = max(curr_sum, ans);
    }

    cout << ans;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/dynamic-programming/kadanes-algorithm-official/ojquestion
