# Problem Statement
1. You are given N number of books. Every ith book has Ai number of pages.
2. You have to allocate books to M number of students. There can be many ways or permutations to do so. In each permutation, one of the M students will be allocated the maximum number of pages. Out of all these permutations, the task is to find that particular permutation in which the maximum number of pages allocated to a student is minimum of those in all the other permutations and print this minimum value.
3. Each book will be allocated to exactly one student. Each student has to be allocated at least one book.
4. Note: Return -1 if a valid assignment is not possible, and allotment should be in contiguous order.

[Tutorial](https://www.youtube.com/watch?v=okP-e2VpI_g&list=PL-Jc9J83PIiHhXKonZxk7gbEWsmSYP5kq&index=23)

# Thought Process
- It _kinda_ uses sliding window technique
- We want to minimize stress on the student with most books
- If we give all books to 1 student hypothetically, then he will have sum(nums) books. This is our `hi`
- The `lo` is the maximum element in nums (why? watch tutorial)
- We do a binary search in this range and find the lowest value for `isPossible`

To check if an arrangement is possible using `isPossible`:
- We start traversing from left
- If sum exceeds our selected `mid`, we add another student
- At the end, we check how many students we have given the books to

# Code
```cpp
bool isPossible(vector<int> nums, int mid, int m) {
    int students = 1, sum = 0;

    for (int i = 0; i < (int)nums.size(); ++i) {
        sum += nums[i];

        if (sum > mid) {
            students++;
            sum = nums[i];
        }
    }

    return students <= m;
}

void solve(vector<int> nums, int m) {
    int ans = 0;
    int sum = accumulate(nums.begin(), nums.end(), 0);
    int mx = *max_element(nums.begin(), nums.end());

    int lo = mx, hi = sum;

    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;

        if (isPossible(nums, mid, m)) {
            ans = mid;
            hi = mid - 1;
        } else {
            lo = mid + 1;
        }
    }

    cout << ans << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/searching-and-sorting/allocate_minimum_number_of_pages/ojquestion
