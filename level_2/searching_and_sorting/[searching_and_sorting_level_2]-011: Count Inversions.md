# Problem Statement
1. Given an array of integers. Find the Inversion Count in the array.
2. For an array, inversion count indicates how far (or close) the array is from being sorted. If array is already sorted then the inversion count is 0. If an array is sorted in the reverse order then the inversion count is the maximum.
3. Formally, two elements a[i] and a[j] form an inversion if a[i] > a[j] and i < j.

[Tutorial](https://www.youtube.com/watch?v=uojx--MK_n0&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=12)

> !! Needs revision and close anaylsis

# Thought Process
- This is almost EXACTLY same as mergesort (watch GFG's mergesort video if you dont remember this)
- At each step while merging, if any element on left is greater than that on right, just increment `cnt`. This is the only extra step in plain mergesort

# Code

> ! Code is flawed

```cpp
int cnt;

vector<int> mergeTwoArrays(vector<int> left, vector<int> right) {
    int i = 0, j = 0, k = 0;

    vector<int> merged(left.size() + right.size());
    while (i < (int)left.size() && j < (int)right.size()) {
        if (left[i] <= right[j]) {
            merged[k] = left[i];
            i++;
            k++;
        } else {
            cnt += ((int)left.size() - i);  // Think why we dont just cnt++;. Hint: because all other elements will also have inversions
            merged[k] = right[j];
            j++;
            k++;
        }
    }

    while (i < (int)left.size()) {
        merged[k] = left[i];
        i++;
        k++;
    }

    while (j < (int)right.size()) {
        merged[k] = left[j];
        j++;
        k++;
    }

    return merged;
}

vector<int> mergeSort(vector<int> nums, int lo, int hi) {
    if (lo == hi) {
        return vector<int>(1, nums[lo]);
    }
    int mid = (lo + hi) / 2;

    vector<int> left = mergeSort(nums, lo, mid);
    vector<int> right = mergeSort(nums, mid + 1, hi);
    vector<int> merged = mergeTwoArrays(left, right);

    return merged;
}

void solve(vector<int> nums, int n) {
    cnt = 0;
    mergeSort(nums, 0, n - 1);
    cout << cnt << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/count_inversions/ojquestion
