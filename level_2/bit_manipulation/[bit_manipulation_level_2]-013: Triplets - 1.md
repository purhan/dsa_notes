# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=sdJBPdoD3OY&list=PL-Jc9J83PIiFJRioti3ZV7QabwoJK6eKe&index=13)

# Thought Process
- Observation to make:
- Whatever is the value of K. if xor(a[i] .... a[k]) == 0, we can choose any j between them and it will be valid
- This is the only scenario we need to check

# Code
```cpp
class Solution {
public:
    int countTriplets(vector<int>& arr) {
        int ans = 0, n = arr.size();
        for(int i = 0; i < n; ++i) {
            int xorr = arr[i];

            for(int k = i + 1; k < n; ++k) {
                xorr ^= arr[k];
                if(xorr == 0) {
                    ans += (k - i);
                }
            }
        }
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/count-triplets-that-can-form-two-arrays-of-equal-xor/
