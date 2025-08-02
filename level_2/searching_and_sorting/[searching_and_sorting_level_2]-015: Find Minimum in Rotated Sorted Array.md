# Problem Statement
1. Suppose an array of length n sorted in ascending order is rotated between 1 and n times.
2. Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]].
3. Given the sorted rotated array nums of unique elements, return the minimum element of this array.
4. You must write an algorithm that runs in O(log n) time.

[Tutorial](https://www.youtube.com/watch?v=Kcj2NGnuSNg&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=15)

# Thought Process
- Do a binary search
- In case `lo` <= `hi`, that array is sorted
- Else:
  - If element is smaller than the previous element, we found the smallest element
  - If element is bigger than next element, we found the smallest element
  - If both above conditions are false, then:
    - if `lo` <= `mid`, do a binary search in right half
    - if `mid` <= `hi`, do a binary search in left half

# Code
```cpp
void solve(vector<int> nums, int n) {
    int lo = 0, hi = n - 1;

    if (nums[lo] <= nums[hi]) {
        cout << nums[0] << endl;
        return;
    }

    while (lo <= hi) {
        int mid = (lo + hi) / 2;

        if (nums[mid] < nums[mid - 1]) {
            cout << nums[mid] << endl;
            return;
        } else if (nums[mid] > nums[mid + 1]) {
            cout << nums[mid + 1] << endl;
            return;
        } else if (nums[lo] <= nums[mid]) {
            lo = mid + 1;
        } else if (nums[mid] <= nums[hi]) {
            hi = mid - 1;
        }
    }
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/find_minimum_in_rotated_sorted_array/ojquestion
- https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/
