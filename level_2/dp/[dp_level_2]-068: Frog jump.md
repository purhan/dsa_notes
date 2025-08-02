# Problem Statement

![image](https://user-images.githubusercontent.com/10897423/144894167-f26e5d94-16e6-425d-ad5f-213a66ce1762.png)

[Tutorial](https://www.youtube.com/watch?v=1V8gRXh1qbU&list=PL-Jc9J83PIiEZvXCn-c5UIBvfT8dA-8EG&index=68)

# Thought Process
- Tutorial had iterative, I solved recursive only

Recursive:
- We need to check if a stone exists at a position. Use map to speed up this operation.
- From each stone, if `k - 1` is positive, we can jump `k - 1`
- From each stone, if `k` is positive, we can jump `k`
- From each stone, we can jump `k + 1`
- Call all 3 of these recursively

# Code
```cpp
class Solution {
    unordered_map<int, bool> stoneExists;
    map<pair<long long, int>, bool> dp;
    int n;
    long long target;

    bool helper(int idx, int k) {
        if(idx == target) return true;
        if(idx > target) return false;
        if(!stoneExists[idx]) return false;

        if(dp.count({idx, k})) return dp[{idx, k}];

        bool res = false;
        if(k > 0)
            res = res || helper(idx + k, k);

        res = res || helper(idx + k + 1, k + 1);

        if(k > 1)
            res = res || helper(idx + k - 1, k - 1);

        return dp[{idx, k}] = res;
    }
public:
    bool canCross(vector<int>& stones) {
        for(auto s: stones) this->stoneExists[s] = true;

        this->n = stones.size();
        this->target = stones[n - 1];
        return helper(0, 0);
    }
};
```

# Problem Links
- https://leetcode.com/problems/frog-jump/
