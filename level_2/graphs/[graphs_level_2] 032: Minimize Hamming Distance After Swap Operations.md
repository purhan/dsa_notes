# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=BQaiNwwxvKY&list=PL-Jc9J83PIiEuHrjpZ9m94Nag4fwAvtPQ&index=32)

# Thought Process
- Construct a DSU for INDECES
- Merge inter-swappable indeces into one group
- In first example in the LC question, we have 2 types of numbers then:
  - Belong to a swappable index
  - Belong to a non-swappable index
- For swappable indeces, just check the number of distinct elements in both vectors (i.e. source and target)
- For non swappable indeces, check the number of all such indeces where the character doesnt match

# Code
```cpp
class Solution {
public:
    int minimumHammingDistance(vector<int>& source, vector<int>& target, vector<vector<int>>& allowedSwaps) {
        int n = target.size();
        DSU dsu(1e5 + 1);

        for(auto swaps: allowedSwaps) {
            dsu.join(swaps[0], swaps[1]);
        }
        map<int, map<int, int>> mp;

        for(int i = 0; i < n; ++i) {
            mp[dsu.getParent(i)][source[i]]++;
            mp[dsu.getParent(i)][target[i]]--;
        }

        int ans = 0;
        for(int i = 0; i < n; ++i) {
            auto mmap = mp[i];
            for(auto [x, freq]: mmap) ans += abs(freq);
        }

        return ans / 2;
    }
};
```

# Problem Links
- https://leetcode.com/problems/minimize-hamming-distance-after-swap-operations/
