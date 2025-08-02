# Problem Statement
1. You are given a number n, representing the size of array a.
2. You are given n numbers, representing elements of array a.
3. The array is nearly sorted. Every element is at-max displaced k spots left or right to it's position in the sorted array. Hence it is being called k-sorted array.
4. You are required to sort and print the sorted array.

Note -> You can use at-max k extra space and nlogk time complexity.

[Tutorial](https://www.youtube.com/watch?v=pptk8cUHHUg&list=PL-Jc9J83PIiHq5rMZasunIR19QG3E-PAA&index=15)

# Thought Process
- Very similar to find k largest elements.
- Uses "priority queue funnel technique"
- Create a priority queue of max size `k`
- Store first k elements of array in it
- Traverse the rest of the array
- With every traversal, store the element in the array. `pq` will sort all its `k + 1` elements itself in `log k`
- Pop from `pq` (will pop the smallest element)
- Time complexity O(nlogk)

# Code
```cpp
void solve(vector<int> nums, int n, int k) {
    priority_queue<int, vector<int>, greater<int>> pq;

    for (int i = 0; i <= k; ++i) {
        pq.push(nums[i]);
    }

    for (int i = k + 1; i < n; ++i) {
        auto t = pq.top();
        if (t < nums[i]) {
            pq.push(nums[i]);
            cout << t << endl;
            pq.pop();
        }
    }

    while (!pq.empty()) {
        auto t = pq.top();
        cout << t << endl;
        pq.pop();
    }
}
```

# Problem Links
https://www.pepcoding.com/resources/online-java-foundation/hashmap-and-heap/sort-ksorted-official/ojquestion
