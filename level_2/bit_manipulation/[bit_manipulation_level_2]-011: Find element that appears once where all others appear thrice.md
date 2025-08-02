# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=3gJxLkPPW6M&list=PL-Jc9J83PIiFJRioti3ZV7QabwoJK6eKe&index=12z)

# Thought Process

2 methods:

one is in O(32 * N)

other is in O(N)

O(32 * N):
- At every bit's position, find the frequency of set bits. If it's divisible by 3, do nothing. If not, that means that our unique number has its bit set at that position

```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        vector<int> bit(32);

        // For each index in bitset, find frequency of set bits for all numbers
        for(int i = 0; i < 32; ++i) {
            for(auto num: nums) {
                if(num & (1 << i)) bit[i]++;
            }
        }

        // For indices where bit frequency is not divisible by 2, turn this bit on in our unique number
        int mask = 0;
        for(int i = 0; i < 32; ++i) {
            if(bit[i] % 3 == 1) mask |= (1 << i);
        }
        return mask;
    }
};
```

O(N) approach:
- Watch tutorial to revise
- We keep 3 numbers, 3n, 3np1 and 3np2

# Problem Links
- https://leetcode.com/problems/single-number-ii/
