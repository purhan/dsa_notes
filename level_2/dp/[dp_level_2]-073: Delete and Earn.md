# Problem Statement

[Tutorial](https://www.youtube.com/watch?v=qVfjmkL1naw&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=73)

# Thought Process
Recursive:

- Think of it as house robber problem
- Saying you can't choose adjacent elements on both sides is exactly like saying you cant choose any 2 adjacent elements (if that makes sense.) Which is exactly the same as house robber problem
- Convert the given array into a frequency map instead of using it as it is, because that would make avoiding adjacent elements more expensive

Iterative:
- No need to use 2D array as we are only checking `last_include` and `last_exclude`

# Code

Recursive:

```cpp
class Solution {
    vector<int> freq;
    vector<int> dp;

    int helper(int idx) {
        if(idx >= freq.size()) return 0;
        if(dp[idx] != -1) return dp[idx];

        int inc = helper(idx + 2) + (idx * freq[idx]);
        int exc = helper(idx + 1);
        return dp[idx] = max(inc, exc);
    }
public:
    int deleteAndEarn(vector<int>& nums) {
        this->dp = vector<int>(10001, -1);
        this->freq = vector<int>(10001, 0);
        for(auto i: nums) this->freq[i]++;
        return helper(0);
    }
};
```

Iterative:

```cpp
class Solution {
public:
    int deleteAndEarn(vector<int>& nums) {
        int last_inc = 0;
        int last_exc = 0;

        int count[10001] = {0};

        for(int val: nums) count[val]++;

        for(int i = 0; i <= 10000; ++i) {
            int inc = last_exc + (count[i] * i);
            int exc = max(last_inc, last_exc);

            last_inc = inc;
            last_exc = exc;
        }
        return max(last_inc, last_exc);
    }
};
```

# Problem Links
- https://leetcode.com/problems/delete-and-earn/
