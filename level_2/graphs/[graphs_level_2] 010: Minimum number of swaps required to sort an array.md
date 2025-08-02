# Problem Statement
Given an array of n distinct elements, find the minimum number of swaps required to sort the array.

[Tutorial](https://www.youtube.com/watch?v=m-8_yQao-lI&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=10)

# Thought Process
- We create a sorted array keeping track of original indices in pair
- We traverse through the sorted array
- If an element is at a position where it was originally (i.e. was sorted already), we do nothing
- If an element has changed position from original array, we start searching from that index. Basically, we DFS/BFS over the elements until we reach a cycle. We then add the `length of the cycle - 1` to the ans.
- Basically, that cycle represents the sequence of swapping those elements so that they are sorted.

![image](https://user-images.githubusercontent.com/10897423/136702685-bd5df0f3-63e9-4d03-99b8-afa9a7eb691d.png)

# Code
```cpp
void solve(vector<int> nums, int n) {
    vector<pair<int, int>> sorted(n);

    for (int i = 0; i < n; ++i) {
        sorted[i].first = nums[i];
        sorted[i].second = i;
    }
    sort(sorted.begin(), sorted.end());

    int ans = 0;
    unordered_map<int, bool> visited;

    for (int i = 0; i < n; ++i) {
        if (visited[i] || sorted[i].second == i) {
            continue;
        }

        int cycle_length = 0;
        int j = i;
        while (!visited[j]) {
            visited[j] = true;
            j = sorted[j].second;
            cycle_length++;
        }

        ans += cycle_length - 1;
    }

    cout << ans;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/graphs/minimum-number-of-swaps-required-to-sort-an-array-official/ojquestion#!