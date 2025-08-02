# Problem Statement
Given an integer array of even length arr, return true if it is possible to reorder arr such that arr[2 * i + 1] = 2 * arr[2 * i] for every 0 <= i < len(arr) / 2, or false otherwise.

[Tutorial](https://www.youtube.com/watch?v=ZOITpH3RDAk&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=38)

# Thought Process
- We have to rearrange numbers such that indeces ((1, 2), (3, 4), (5, 6)....) have values {k, 2*k}. (eg: 1,2, 1,2, 4,8, 3,6)
- First we sort the array (little modified sorting, if array has negative numbers, first negative numbers will be sorted by absolute value) For example: `-1, -2, -3, -4, 1, 2, 3, 4, 6`. Normal sorting wouldve given `-4, -3, -2, -1, 1, 2, 3, 4, 6`

- Now traversing the array, we have to check for every number, if its double value exists in the array (use map to do this in O(1)). Then, virtually mark those numbers as 'used' so we don't use them again

- Example case:
```
array: 3, 6, 2, 4, 3, 6

=> 2, 4, 3, 3, 6, 6

=> 2, 4, 3, 3, 6, 6
   x  x

=> 2, 4, 3, 3, 6, 6
   x  x  x     x

=> 2, 4, 3, 3, 6, 6
   x  x  x  x  x  x
```

# Code
```cpp
class Solution {
    static bool comp(int &a, int &b) {
        if(a < 0 && b < 0) {
            return a > b;
        }
        return a < b;
    }
public:
    bool canReorderDoubled(vector<int>& arr) {
        sort(arr.begin(), arr.end(), comp);
        map<int, int> cnt;
        for(auto i: arr) cnt[i]++;

        for(auto i: arr) {
            if(cnt[i] == 0)
                continue;

            cnt[i]--;
            cnt[2 * i]--;

            if(cnt[i] == -1 || cnt[2 * i] == -1)
                return false;
        }

        return true;
    }
};
```

# Problem Links
- https://leetcode.com/problems/array-of-doubled-pairs/
