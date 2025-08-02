# Problem Statement
1. Given an unsorted array 'arr'.
2. Reorder it in-place such that :  arr[0] , arr[1], arr[2], arr[3] . . . . arrange in zigzag manners, watch video for this point.
3. Please sort the array in place and do not define additional arrays.
4. Allowed Time Complexity: O(n)

[Tutorial](https://www.youtube.com/watch?v=eOlp2q08EDU&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=27)

# Thought Process
- For odd positions, we want the element to be bigger than next element. If not already, swap with next element.
- For even positions, we want the element to be smaller than next element. If not already, swap with next element.

Alternative approach, also useful for wiggle sort 2:
- Sort the array
- Place one element from front, next from back, next from front, and so on

# Code
```cpp
void solve(vector<int> nums, int n) {
    for (int i = 0; i < n - 1; ++i) {
        if (i & 1) {    // checking `is i odd` but position here is even (because 0 indexing)
            if (nums[i] < nums[i + 1]) swap(nums[i], nums[i + 1]);
        } else {
            if (nums[i] > nums[i + 1]) swap(nums[i], nums[i + 1]);
        }
    }

    for (auto i : nums) cout << i << " ";
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/arrays-and-strings/wiggle-sort-1/ojquestion#!