# Problem Statement
1. You are given a number n, representing the size of array a.
2. You are given n numbers, representing elements of array a.
3. You are given a number k.
4. You are required to find and print the k largest elements of array in increasing order.

[Tutorial](https://www.youtube.com/watch?v=taL2G6jDLog&list=PL-Jc9J83PIiHq5rMZasunIR19QG3E-PAA&index=12)

# Thought Process
- Create a priority queue of max size `k`
- Store first k elements of array in it
- Traverse the rest of the array
- If the element is greater than the smallest element in `pq`, then replace it with that. Else do nothing
- In the end, print the `pq`

# Code
```cpp
void solve(vector<int> nums, int n, int k) {
    priority_queue<int, vector<int>, greater<int>> pq;

    for (int i = 0; i < k; ++i) {
        pq.push(nums[i]);
    }

    for (int i = k; i < n; ++i) {
        auto t = pq.top();
        if (t < nums[i]) {
            pq.push(nums[i]);
            pq.pop();
        }
    }

    while (!pq.empty()) {
        auto t  = pq.top();
        pq.pop();
        cout << t << endl;
    }
}
```

# Problem Links
https://www.pepcoding.com/resources/online-java-foundation/hashmap-and-heap/k-largest-elements-official/ojquestion
