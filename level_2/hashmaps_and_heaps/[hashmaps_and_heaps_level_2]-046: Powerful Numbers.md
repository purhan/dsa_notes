# Problem Statement
Given three integers x, y, and bound, return a list of all the powerful integers that have a value less than or equal to bound.

An integer is powerful if it can be represented as xi + yj for some integers i >= 0 and j >= 0.

You may return the answer in any order. In your answer, each value should occur at most once.

[Tutorial](https://www.youtube.com/watch?v=PniLCiboQ8E&list=PL-Jc9J83PIiEp9DKNiaQyjuDeg3XSoVMR&index=46)

# Thought Process
- `x^i` will never cross bound, because `x^i + y^j <= bound` and `y^j` will be atleast 1
- similarly, `y^j` will never cross bound
- we can bruteforce loop over all powers of x and y. Mathematically, x^i and y^j will never be too big (only 20 power for given constraints) so we can double-loop

# Code
```cpp
class Solution {
public:
    vector<int> powerfulIntegers(int x, int y, int bound) {
        unordered_set<int> s;

        for(int i = 1; i < bound; i *= x) {
            for(int j = 1; i + j <= bound; j *= y) {
                s.insert(i + j);
                if(y == 1) break;
            }
            if(x == 1) break;
        }

        vector<int> ans;
        for(auto i: s) ans.push_back(i);
        return ans;
    }
};
```

# Problem Links
- https://leetcode.com/problems/powerful-integers/
