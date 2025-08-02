# Problem Statement
1. We have arrival and departure times of all trains that reach a railway station. 
2. We have to find the minimum number of platforms required for the railway station so that no train is kept waiting.
3. Consider that all the trains arrive on the same day and leave on the same day. 
4. Arrival and departure time can never be the same for a train but we can have arrival time of one train equal to departure time of the other. 
5. At any given instance of time, same platform can not be used for both departure of a train and arrival of another train. In such cases, we need different platforms.

[Tutorial](https://www.youtube.com/watch?v=FkJZlZHWUyk&list=PL-Jc9J83PIiE-TR27GB7V5TBLQRT5RnSl&index=67)

# Thought Process
- At any point, we want to know the total number trains at the station
- The maximum number of trains at any point is the ans
- I solved this a lil different from the tutorial but the idea is the exact same
- Put arrival and departure times in a vector<pair> along with `1 or -1 for arrival or departure respectively`
- Traverse through the new array, for arrival, add 1, for departure subtract 1

- Instead of creating a new array, we could use 2 pointers on both sorted arrays

# Code
```cpp
void solve(int n, vector<int> arrival, vector<int> departure) {
    vector<pair<int, int>> t;
    for (int i = 0; i < n; ++i) t.push_back({arrival[i], 1});
    for (int i = 0; i < n; ++i) t.push_back({departure[i], -1});
    sort(t.begin(), t.end());

    int ans = 0, cnt = 0;
    for (int i = 0; i < 2 * n; ++i) {
        cnt += t[i].second;
        ans = max(ans, cnt);
    }

    cout << ans << endl;
}
```

# Problem Links
- https://www.pepcoding.com/resources/data-structures-and-algorithms-in-java-levelup/arrays-and-strings/minimum-number-of-platform/ojquestion
