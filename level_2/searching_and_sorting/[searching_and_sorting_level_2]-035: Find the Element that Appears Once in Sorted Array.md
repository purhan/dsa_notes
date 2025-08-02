# Problem Statement
Given a sorted array arr[] of size N. Find the element that appears only once in the array. All other elements appear exactly twice.

[Tutorial](https://www.youtube.com/watch?v=WFNa5o-dHGo&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=35)

# Thought Process
- Do a binary search
- Depending on whether `mid` is even or odd, we check the conditions.

# Code
```cpp
void solve(vector<int> nums, int n) {
    // dont worry, base cases on extreme ends of array
    if (nums[0] != nums[1]) {
        cout << nums[0] << endl;
        return;
    } else if (nums[n - 1] != nums[n - 2]) {
        cout << nums[n - 1] << endl;
        return;
    }

    int lo = 0, hi = n - 1;
    int ans = 0;


    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;

        if (nums[mid] != nums[mid + 1] && nums[mid] != nums[mid - 1]) {
            ans = nums[mid];
            break;
        }

        if (mid & 1) {
            if (nums[mid] == nums[mid - 1]) {
                lo = mid + 1;
            } else {
                hi = mid - 1;
            }
        } else {
            if (nums[mid] == nums[mid + 1]) {
                lo = mid + 1;
            } else {
                hi = mid - 1;
            }
        }
    }

    cout << ans << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/find-the-element-that-appears-once-in-sorted-array--offcial/ojquestion
