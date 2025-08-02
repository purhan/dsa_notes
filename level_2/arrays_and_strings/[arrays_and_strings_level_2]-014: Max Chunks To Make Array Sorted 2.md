# Problem Statement

Same as max chunks 1, only difference being, there, the elements were permutation of n, here elements are random. Our solution works for both

[Tutorial]()

> Same solution works for max chunks 1

> ! Remember to checkout Trapping Rainwater Problem

# Thought Process

Two ways to do this
- Sort the array, keep index paired with elements
- Use chaining technique to check which chunks have elements that are sorted within that chunk only (i.e. look for chunks in which all elements are same before and after sorting)
- Print the count of all such chunks

Second method
- Use range queries and store maxLeft and minRight at each index
- If at any point, `maxLeft <= minRight`, that means that the subarray to its right and the subarray to its left are valid chunks (think ?)
- Print count of all such points

# Code
```cpp
class Solution {
public:
    int maxChunksToSorted(vector<int>& arr) {
        int n = size(arr);
        vector<int> leftMax(n), rightMin(n);

        int mx = -1;
        for(int i = 0; i < n; ++i) {
            mx = max(mx, arr[i]);
            leftMax[i] = mx;
        }

        int mn = INT_MAX;
        for(int i = n - 1; i >= 0; --i) {
            mn = min(mn, arr[i]);
            rightMin[i] = mn;
        }

        int ans = 1;
        for(int i = 0; i < n - 1; ++i) {
            if(leftMax[i] <= rightMin[i + 1]) ans++;
        }

        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/max-chunks-to-make-sorted-ii/
